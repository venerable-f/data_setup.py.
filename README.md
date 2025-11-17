import sqlite3

# 1. Connect to the database file. If it doesn't exist, it will be created.
conn = sqlite3.connect('lab_results.db')
cursor = conn.cursor()

# 2. Create the 'results' table (SQL DDL - Data Definition Language)
cursor.execute('''
    CREATE TABLE IF NOT EXISTS results (
        patient_id INTEGER PRIMARY KEY,
        hgb_value REAL,
        test_date TEXT
    )
''')

# 3. Define the data rows (simulated patient results)
data_to_insert = [
    (1, 14.2, '2025-11-01'),
    (2, 11.5, '2025-11-05'),
    (3, 16.8, '2025-11-10'),
    (4, 13.0, '2025-11-15')
]

# 4. Insert the data into the table (SQL DML - Data Manipulation Language)
cursor.executemany("INSERT INTO results VALUES (?, ?, ?)", data_to_insert)

# 5. Save changes and close the connection
conn.commit()
conn.close()

print("Database 'lab_results.db' created and populated successfully.")
