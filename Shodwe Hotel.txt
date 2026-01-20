-- dim_date
CREATE TABLE dim_date (
    date DATE PRIMARY KEY,
    mmm_yy VARCHAR(10),
    week_no INT,
    day_type VARCHAR(20)
);

-- dim_hotels
CREATE TABLE dim_hotels (
    property_id INT PRIMARY KEY,
    property_name VARCHAR(100),
    category VARCHAR(50),
    city VARCHAR(50)
);

-- dim_rooms
CREATE TABLE dim_rooms (
    room_id VARCHAR(10) PRIMARY KEY,
    room_class VARCHAR(50)
);

-- fact_aggregated_bookings
CREATE TABLE fact_aggregated_bookings (
    property_id INT,
    check_in_date DATE,
    room_category VARCHAR(50),
    successful_bookings INT,
    capacity INT,
    PRIMARY KEY (property_id, check_in_date, room_category)
);

-- fact_bookings
CREATE TABLE fact_bookings (
    booking_id VARCHAR(50) PRIMARY KEY,
    property_id INT,
    booking_date DATE,
    check_in_date DATE,
    checkout_date DATE,
    no_guests INT,
    room_category VARCHAR(50),
    booking_platform VARCHAR(50),
    ratings_given DECIMAL(2,1),
    booking_status VARCHAR(30),
    revenue_generated DECIMAL(12,2),
    revenue_realized DECIMAL(12,2),
    customer_id INT,
    payment_method VARCHAR(30),
    stay_duration INT,
    cancellation_reason VARCHAR(100),
    is_loyalty_member BOOLEAN,
    country VARCHAR(50),
    customer_age INT,
    special_requests TEXT,
    discount_applied DECIMAL(5,2),
    booking_channel VARCHAR(50)
);


-- 1. Total Revenue
SELECT 
    SUM(revenue_realized) AS total_revenue
FROM fact_bookings
WHERE booking_status = 'Checked Out'
  AND revenue_realized IS NOT NULL;

-- 2️. Occupancy Rate
SELECT 
    ROUND(
        SUM(successful_bookings)::DECIMAL 
        / SUM(capacity) * 100,
        2
    ) AS occupancy_rate_percentage
FROM fact_aggregated_bookings;

-- 3. Cancellation Rate
SELECT 
    ROUND(
        COUNT(*) FILTER (WHERE booking_status = 'Cancelled')::DECIMAL
        / COUNT(*) * 100,
        2
    ) AS cancellation_rate_percentage
FROM fact_bookings;

-- 4. Total Bookings
SELECT 
    COUNT(booking_id) AS total_bookings
FROM fact_bookings
WHERE booking_status = 'Checked Out';

-- 5. Utilized Capacity
SELECT 
    SUM(successful_bookings) AS utilized_capacity
FROM fact_aggregated_bookings;

-- 6. Trend Analysis (Revenue Over Time)
SELECT 
    d.mmm_yy,
    SUM(f.revenue_realized) AS total_revenue
FROM fact_bookings f
JOIN dim_date d
    ON f.check_in_date = d.date
WHERE f.booking_status = 'Checked Out'
GROUP BY d.mmm_yy
ORDER BY d.mmm_yy;

-- 7. Weekday & Weekend Revenue and Bookings
SELECT 
    d.day_type,
    COUNT(f.booking_id) AS total_bookings,
    SUM(f.revenue_realized) AS total_revenue
FROM fact_bookings f
JOIN dim_date d
    ON f.check_in_date = d.date
WHERE f.booking_status = 'Checked Out'
GROUP BY d.day_type;

-- 8.Revenue by City & Hotel
SELECT 
    h.city,
    h.property_name,
    SUM(f.revenue_realized) AS total_revenue
FROM fact_bookings f
JOIN dim_hotels h
    ON f.property_id = h.property_id
WHERE f.booking_status = 'Checked Out'
GROUP BY h.city, h.property_name
ORDER BY total_revenue DESC;

-- 9. Class Wise Revenue
SELECT 
    room_category,
    SUM(revenue_realized) AS total_revenue
FROM fact_bookings
WHERE booking_status = 'Checked Out'
GROUP BY room_category
ORDER BY total_revenue DESC;

-- 10. Checked Out / Cancel / No Show Breakdown
SELECT 
    booking_status,
    COUNT(*) AS total_bookings
FROM fact_bookings
GROUP BY booking_status;

-- 11. Weekly Trend – Key Metrics
SELECT 
    d.week_no,
    COUNT(f.booking_id) AS total_bookings,
    SUM(f.revenue_realized) AS total_revenue
FROM fact_bookings f
JOIN dim_date d
    ON f.check_in_date = d.date
WHERE f.booking_status = 'Checked Out'
GROUP BY d.week_no
ORDER BY d.week_no;

-- 12. Customer Repeat Rate
SELECT 
    ROUND(
        COUNT(DISTINCT customer_id)::DECIMAL
        / COUNT(customer_id) * 100,
        2
    ) AS repeat_customer_rate
FROM fact_bookings
WHERE booking_status = 'Checked Out';

