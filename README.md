📂 File-Creator

File-Creator is a Python-based utility that automates the creation of files in multiple formats such as .txt, .csv, .json, and .xml.
It is designed to streamline repetitive tasks for developers, data analysts, and system administrators by allowing quick file generation with customizable content.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🚀 Features

✔️ Multi-format Support – Create .txt, .csv, .json, .xml files with one script.
✔️ Custom Content Input – Accepts dynamic user input or reads data from other sources.
✔️ Batch File Creation – Generate multiple files at once for testing or automation.
✔️ Data Validation – Ensures correct structure for CSV and JSON formats.
✔️ Cross-Platform – Works seamlessly on Windows, Linux, and macOS.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🧠 Tech Stack

Language: Python 3.x

Libraries: os, json, csv, argparse

Platform: Cross-platform (CLI utility)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🔧 Setup & Installation
1. Clone the Repository
git clone https://github.com/<your-username>/file-creator.git
cd file-creator

2. Install Requirements (if any)
pip install -r requirements.txt

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🧪 Usage
Run the script:
python file_creator.py --type txt --name sample --content "Hello, world!"

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
Example commands:

Create a text file:

python file_creator.py --type txt --name notes --content "This is a test file."


Create a CSV file:

python file_creator.py --type csv --name dataset --content "id,name,age\n1,John,25\n2,Alice,30"


Create a JSON file:

python file_creator.py --type json --name config --content '{"theme":"dark","version":1.0}'

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
📁 Project Structure
file-creator/
├── file_creator.py             # Main script
├── examples/                   # Example generated files
├── requirements.txt            # Dependencies (if needed)
└── README.md                   # Documentation

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
📊 Example Output

Text File:

Hello, world!

CSV File:

id,name,age
1,John,25
2,Alice,30


JSON File:

{
  "theme": "dark",
  "version": 1.0
}

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
📌 Known Issues

⚠️ JSON content must be valid JSON format.
⚠️ Large batch creation may require elevated file permissions.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🤝 Contributing

Contributions are welcome! Please follow these steps:

Fork the repo

Create a feature branch (git checkout -b feature-name)

Commit changes (git commit -m 'Add new feature')

Push to your branch (git push origin feature-name)

Open a Pull Request

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


CREATE TABLE IF NOT EXISTS csv_configuration
(
    config_id   SERIAL PRIMARY KEY,
    config_name VARCHAR NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS fields
(
    field_id        SERIAL PRIMARY KEY,
    config_id       INT,
    field_name      VARCHAR NOT NULL,
    field_type      VARCHAR NOT NULL,
    is_null_allowed VARCHAR(2),
    pattern         VARCHAR,
    fixed_length    INT,
    min_length      INT,
    max_length      INT,
    CONSTRAINT fk_config
        FOREIGN KEY (config_id)
            REFERENCES csv_configuration (config_id)
            ON DELETE CASCADE
);

CREATE TABLE IF NOT EXISTS allowed_values
(
    value_id   SERIAL PRIMARY KEY,
    field_id   INT,
    value_name VARCHAR NOT NULL,
    CONSTRAINT fk_field_id
        FOREIGN KEY (field_id)
            REFERENCES fields (field_id)
            ON DELETE CASCADE
);

CREATE TABLE IF NOT EXISTS csv_configuration
(
    config_id   SERIAL PRIMARY KEY,
    config_name VARCHAR NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS fields
(
    field_id        SERIAL PRIMARY KEY,
    config_id       INT,
    field_name      VARCHAR NOT NULL,
    field_type      VARCHAR NOT NULL,
    is_null_allowed VARCHAR(2),
    pattern         VARCHAR,
    fixed_length    INT,
    min_length      INT,
    max_length      INT,
    CONSTRAINT fk_config
        FOREIGN KEY (config_id)
            REFERENCES csv_configuration (config_id)
            ON DELETE CASCADE
);

CREATE TABLE IF NOT EXISTS allowed_values
(
    value_id   SERIAL PRIMARY KEY,
    field_id   INT,
    value_name VARCHAR NOT NULL,
    CONSTRAINT fk_field_id
        FOREIGN KEY (field_id)
            REFERENCES fields (field_id)
            ON DELETE CASCADE
);
