#algorithms

> [!quote] Definition
> Kalman Filters can be thought of as a **recursive state estimator**. It is an algorithm, belonging to the domains of _statistics_ and _control theory_, which uses a series of measurements observed over time to produce estimates of unknown variables that tend to be more accurate than those based on a single measurement.

### The Basics of Kalman Filters
Kalman Filters are commonly found in robotics as well as control theories, especially in **robot motion planning and control**. It resembles a common **[[sensor fusion]]** and **data fusion** algorithm.

The foundation of the KF algorithm is as follows:
$Current State = Previous State + K * (Measurement - Predicted Measurement)$

