📂 File-Creator

A Python-based Utility for Automated Multi-format File Generation

Modern developers, analysts, and system administrators frequently deal with file generation. Whether it’s preparing dummy datasets for testing, creating configuration files for deployments, or simply automating repetitive file creation tasks, the need for a versatile file generation tool is universal.

File-Creator is a Python-powered utility designed to automate the creation of files in multiple formats, including .txt, .csv, .json, and .xml. With a flexible command-line interface (CLI), batch creation support, and built-in data validation, File-Creator streamlines workflows and helps teams save countless hours of manual work.

This document provides a comprehensive guide to File-Creator: its features, installation, usage, example commands, database schema integration for advanced CSV validation, and contribution guidelines.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🚀 Features

✔️ Multi-format File Support

Create files in .txt, .csv, .json, and .xml formats with a single script.

Useful for developers who need quick mock data, testers who require multiple file types, and admins generating repetitive configuration files.

✔️ Custom Content Input

Accepts dynamic input directly from the command line.

Reads data from files or external sources (planned feature in roadmap).

Provides flexibility in formatting, such as line breaks in .txt or hierarchical structure in .json and .xml.

✔️ Batch File Creation

Generate multiple files at once using simple loops or arguments.

Useful for creating large test datasets quickly.

✔️ Data Validation

Ensures proper structure for CSV and JSON files.

Invalid JSON raises descriptive errors.

CSV validation integrates with an optional database schema (explained below).

✔️ Cross-Platform Compatibility

Works seamlessly across Windows, Linux, and macOS.

Requires only Python and built-in libraries (with minimal dependencies).

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🧠 Tech Stack

Language: Python 3.x

Core Libraries:

os → file operations

json → JSON serialization and validation

csv → CSV file handling

argparse → CLI argument parsing

🔧 Setup & Installation
1. Clone the Repository
git clone https://github.com/<your-username>/file-creator.git
cd file-creator

2. Install Dependencies (if required)
pip install -r requirements.txt

3. Verify Installation
python file_creator.py --help

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🧪 Usage Examples

Run the script with format type, filename, and content:

python file_creator.py --type txt --name sample --content "Hello, world!"

Example Commands
Create a Text File
python file_creator.py --type txt --name notes --content "This is a test file."


Generated notes.txt:

This is a test file.

Create a CSV File
python file_creator.py --type csv --name dataset --content "id,name,age\n1,John,25\n2,Alice,30"


Generated dataset.csv:

id,name,age
1,John,25
2,Alice,30

Create a JSON File
python file_creator.py --type json --name config --content '{"theme":"dark","version":1.0}'


Generated config.json:

{
  "theme": "dark",
  "version": 1.0
}

Create an XML File
python file_creator.py --type xml --name settings --content "<settings><theme>dark</theme></settings>"


Generated settings.xml:

<settings>
  <theme>dark</theme>
</settings>

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


📁 Project Structure
file-creator/
├── file_creator.py             # Main script
├── examples/                   # Example generated files
├── requirements.txt            # Dependencies (if needed)
└── README.md                   # Documentation

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


📊 Example Outputs

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


XML File:

<root>
  <item>Hello</item>
</root>

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🛢️ Database Schema for CSV Validation

File-Creator supports advanced CSV validation by integrating with a relational database schema. This schema enforces rules such as allowed values, data types, length restrictions, and nullability.

Here’s the schema:

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

🔎 Schema Explanation

csv_configuration

Stores reusable CSV validation configurations.

Each configuration represents a specific CSV format (e.g., employee dataset, product catalog).

fields

Defines columns for each CSV configuration.

Attributes include:

field_name: Name of the column.

field_type: Data type (string, int, date, etc.).

is_null_allowed: Whether the column can be left empty (Y/N).

pattern: Regex pattern for validation (e.g., email format).

fixed_length: For strict length fields (e.g., 10-digit phone numbers).

min_length and max_length: For variable length validation.

allowed_values

Stores a list of permitted values for certain fields.

Example: For a gender field, allowed values could be "Male", "Female", "Other".

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🧩 Example Use Case

CSV Type: Employee Dataset

Configuration Name: employee_csv

INSERT INTO csv_configuration (config_name) VALUES ('employee_csv');


Fields:

INSERT INTO fields (config_id, field_name, field_type, is_null_allowed, pattern, fixed_length, min_length, max_length)
VALUES
(1, 'employee_id', 'int', 'N', NULL, NULL, 1, 10),
(1, 'email', 'string', 'N', '^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$', NULL, 5, 100),
(1, 'phone', 'string', 'Y', '^[0-9]{10}$', 10, 10, 10);


Allowed Values Example:

INSERT INTO allowed_values (field_id, value_name) VALUES (1, '1001');
INSERT INTO allowed_values (field_id, value_name) VALUES (1, '1002');


When a CSV file is generated using File-Creator, this schema ensures strict compliance with predefined validation rules.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


📌 Known Issues

⚠️ JSON content must be valid JSON, otherwise it raises an error.
⚠️ Large batch file creation may require elevated permissions.
⚠️ XML structure validation is minimal in the current version.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


📖 Use Cases

Developers – Generate mock configuration files during development.

Testers – Create thousands of test files quickly.

Data Analysts – Automate creation of structured datasets.

System Administrators – Script-driven creation of logs, configs, and reports.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


📜 Roadmap

✅ Integration with databases for automatic file validation.

✅ Bulk file creation using config files.

✅ XML schema validation (XSD support).

✅ GUI version for non-technical users.

✅ Cloud storage integration (AWS S3, Azure Blob).

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🤝 Contributing

Contributions are welcome!

Fork the repository

Create a feature branch

git checkout -b feature-xml-schema


Commit your changes

git commit -m "Add XML schema validation"


Push to your branch

git push origin feature-xml-schema


Submit a Pull Request

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


🛡️ Final Thoughts

File-Creator simplifies a task that is often underestimated: creating structured files quickly and consistently. With multi-format support, batch generation, and optional schema-based validation, it fits perfectly into the workflows of developers, testers, analysts, and IT administrators.

By combining automation, validation, and flexibility, File-Creator ensures that teams spend less time on repetitive tasks and more time focusing on innovation.

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
