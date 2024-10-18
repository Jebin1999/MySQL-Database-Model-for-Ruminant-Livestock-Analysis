

# Ruminant Livestock Management MySQL Database

## Overview

This project showcases the use of **MySQL** for managing and analyzing ruminant livestock data, specifically focusing on **dairy farming**. The database stores and tracks data for individual cows, daily feed intake, milk yield, and health records. This structure enables **data-driven decision-making** in dairy farming by providing insights into how feed intake impacts milk yield, detecting trends in milk production, and monitoring cow health for early disease detection.

### Key Features:
- **Cows Data**: Store information such as breed, lactation stage, and health status for each cow.
- **Feed Intake Data**: Track daily feed consumption, including the nutritional content (protein, fat, energy).
- **Milk Yield Data**: Record daily milk production in liters, along with fat and protein content of the milk.
- **Health Records**: Monitor health metrics such as temperature, heart rate, disease diagnoses, and treatments.
- **Feed Cost Analysis (Optional)**: Analyze feed costs to optimize feed intake in relation to milk yield.

### Goals:
- **Understand the relationship between feed intake and milk yield** by analyzing historical data.
- **Monitor cow health** and identify abnormal patterns (e.g., detecting diseases early based on health records).
- **Optimize feed efficiency** by analyzing costs and nutrient impacts on milk production.

---

## Database Structure

The database consists of five main tables:

1. **Cows Table**:
   - Stores basic information about each cow (e.g., breed, age, lactation stage).
   - Fields: `cow_id`, `cow_name`, `breed`, `birth_date`, `lactation_stage`, `age`, `health_status`.

2. **Feed Intake Table**:
   - Tracks daily feed intake for each cow, including the nutritional composition (protein, fat, energy).
   - Fields: `intake_id`, `cow_id`, `intake_date`, `feed_type`, `amount_kg`, `protein_percent`, `fat_percent`, `energy_mj`.

3. **Milk Yield Table**:
   - Records daily milk yield for each cow, including milk fat and protein content.
   - Fields: `yield_id`, `cow_id`, `yield_date`, `milk_yield_liters`, `fat_content_percent`, `protein_content_percent`.

4. **Health Records Table**:
   - Monitors cow health, tracking metrics such as body temperature, heart rate, and treatments.
   - Fields: `health_id`, `cow_id`, `record_date`, `temperature`, `heart_rate`, `disease`, `treatment`.

5. **Feed Costs Table (Optional)**:
   - Stores cost data for each type of feed to analyze cost-effectiveness.
   - Fields: `feed_type`, `cost_per_kg`.

---

## Installation and Setup

### Prerequisites:
- MySQL installed on your local machine.
- Access to MySQL client or any GUI like MySQL Workbench for running SQL queries.

### Steps:

1. **Clone the Repository**:
   Clone this repository to your local machine using:
   ```bash
   git clone https://github.com/yourusername/livestock_mysql_project.git
   ```

2. **Create the Database**:
   Create the database and tables by running the SQL script `create_tables.sql` provided in the `SQL/` directory:
   ```sql
   SOURCE /path_to_project/livestock_mysql_project/SQL/create_tables.sql;
   ```

3. **Insert Sample Data**:
   You can insert sample data into the tables by running the `insert_sample_data.sql` script in the `SQL/` directory:
   ```sql
   SOURCE /path_to_project/livestock_mysql_project/SQL/insert_sample_data.sql;
   ```

4. **Run Queries**:
   Use the queries in the `queries.sql` file to perform analysis. For example, you can calculate total milk yield per cow or analyze the relationship between feed intake and milk yield:
   ```sql
   SOURCE /path_to_project/livestock_mysql_project/SQL/queries.sql;
   ```

---

## Usage

Once the database is set up and populated with data, you can run a variety of **SQL queries** to analyze the livestock data. Here are a few example queries:

### 1. **Total Milk Yield per Cow**:
   This query calculates the total amount of milk each cow has produced over a given time period.
   ```sql
   SELECT 
       cow_id, 
       SUM(milk_yield_liters) AS total_milk_yield 
   FROM 
       milk_yield
   WHERE 
       yield_date BETWEEN '2024-01-01' AND '2024-12-31'
   GROUP BY 
       cow_id;
   ```

### 2. **Average Feed Intake per Cow**:
   This query calculates the average daily feed intake and the nutritional breakdown for each cow.
   ```sql
   SELECT 
       cow_id,
       AVG(amount_kg) AS avg_feed_amount_kg,
       AVG(protein_percent) AS avg_protein_percent,
       AVG(fat_percent) AS avg_fat_percent,
       AVG(energy_mj) AS avg_energy_mj
   FROM 
       feed_intake
   WHERE 
       intake_date BETWEEN '2024-01-01' AND '2024-12-31'
   GROUP BY 
       cow_id;
   ```

### 3. **Health Status and Milk Yield**:
   This query identifies cows with abnormal health metrics (e.g., high temperature or low milk yield) and includes their recent health records.
   ```sql
   SELECT 
       h.cow_id, 
       h.record_date, 
       h.temperature, 
       h.disease, 
       m.milk_yield_liters
   FROM 
       health_records h
   JOIN 
       milk_yield m 
       ON h.cow_id = m.cow_id AND h.record_date = m.yield_date
   WHERE 
       h.temperature > 39.0  -- Abnormally high temperature
       OR m.milk_yield_liters < 10;  -- Low milk yield threshold
   ```

---

## Future Enhancements

1. **Advanced Analytics**:
   - Implement **feed cost optimization** by integrating cost analysis for each feed type.
   - Use machine learning models to predict milk yield based on feed intake, health, and environmental factors.

2. **Integration with R**:
   - Connect this database with R or Python to perform advanced statistical analysis and visualizations, including time series analysis and regression models.

3. **Interactive Dashboards**:
   - Develop a front-end application using **Shiny (R)** or **Dash (Python)** to display live data on cow health, milk yield trends, and feed optimization.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

Special thanks to open-source data contributors and the dairy farming community for providing the inspiration for this project.

