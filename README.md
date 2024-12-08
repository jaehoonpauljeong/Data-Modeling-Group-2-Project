# Data-Modeling-Group-2-Project
This is the Term Project for the Course entitled Data Modeling for Intelligent Networks and Security (ESW7002-41), Fall 2024.

## Overview
This repository contains the implementation of an AI-driven solution to automate security policy generation. Using OpenAI's GPT-4o-mini language model, the system translates natural language descriptions into XML policies compliant with the I2NSF (Interface to Network Security Functions) Consumer-Facing Interface. This project aims to simplify network security configuration for non-technical users by automating the creation of machine-readable, standards-compliant security policies.

## Features
- **Natural Language to XML Translation**: Converts user-friendly policy descriptions into structured XML policies.
- **I2NSF Compliance**: Generates policies following the I2NSF Consumer-Facing Interface schema.
- **Ease of Use**: Enables non-technical users to define high-level security policies.
- **Event-Condition-Action Model**: Supports defining conditions (e.g., time, URL categories) and actions (e.g., blocking or allowing traffic).

## System Architecture
The implementation leverages the following key components:
1. **Natural Language Understanding**: Processes user input to identify key components like events, conditions, and actions.
2. **Prompt Engineering**: Utilizes a tailored prompt to guide the GPT-4o-mini model in generating XML outputs compliant with the I2NSF schema.
3. **YANG Data Model Integration**: Incorporates the standardized Consumer-Facing Interface schema to ensure output interoperability and consistency.

![System Diagram](path/to/system_diagram.png)

## Example
Input: _"Block SNS access during office hours with a weekly frequency (9am-5pm; Monday-Friday)."_

Generated Output:
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<i2nsf-cfi-policy xmlns="urn:ietf:params:xml:ns:yang:ietf-i2nsf-cfi-policy">
    <name>block_sns_access_during_office_hours</name>
    <rules>
        <name>block_sns_access</name>
        <condition>
            <time>
                <frequency>weekly</frequency>
                <period>
                    <start-time>09:00</start-time>
                    <end-time>17:00</end-time>
                    <day>Monday</day>
                    <day>Tuesday</day>
                    <day>Wednesday</day>
                    <day>Thursday</day>
                    <day>Friday</day>
                </period>
            </time>
            <url-category>
                <url-name>SNS</url-name>
            </url-category>
        </condition>
        <actions>
            <primary-action>
                <action>drop</action>
            </primary-action>
        </actions>
    </rules>
</i2nsf-cfi-policy>
```

## Getting Started

### Prerequisites
- Python 3.8+
- OpenAI API Access
- Jupyter Notebook (for running the provided `.ipynb` file)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/automated-security-policy-gen.git
   cd automated-security-policy-gen
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Usage
1. Open the Jupyter Notebook `natural-language-to-security-policy.ipynb`.
2. Replace the OpenAI API key placeholder with your key.
3. Input your desired policy descriptions and run the cells to generate XML policies.

## Project Structure
- **`natural-language-to-security-policy.ipynb`**: Main implementation notebook.
- **`README.md`**: Documentation of the project.
- **`examples/`**: Directory containing example input and output policies.
- **`requirements.txt`**: Python dependencies.

## Contributing
Contributions are welcome! Please submit a pull request or open an issue for bug fixes, feature requests, or improvements.

## Future Work
- Expand datasets for quantitative evaluation of generated policies.
- Enhance model scalability and context awareness for diverse cybersecurity scenarios.
- Integrate the implementation with I2NSF systems for end-to-end functionality.

## Authors
- Mikel Larrarte Rodriguez, Jorge Alcorta Berasategui, Jaehoon (Paul) Jeong

## License
This project is licensed under the [MIT License](LICENSE).

## References
- [I2NSF Consumer-Facing Interface YANG Data Model](https://datatracker.ietf.org/doc/draft-ietf-i2nsf-consumer-facing-interface-dm/31/)
- OpenAI GPT-4o-mini Documentation

