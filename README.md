# Remote device status check

Network device monitoring test with SSH tunneling and CSV parsing.

## Task description

This exercise requires the development of a Python test suite designed to monitor the operational status of network devices. The test must establish an SSH tunnel to a remote server, referred to as Server B, via an intermediary server, Server A, given that direct network connectivity to Server B is unavailable. The IP addresses of Server A and Server B, along with their respective SSH private keys, will be provided as environment variables: SERVER_A_ADDRESS, SERVER_B_ADDRESS, SERVER_A_KEY, and SERVER_B_KEY. The SSH tunnel will be established programmatically, with authentication performed for the user "stauto".

Upon successful tunnel establishment, the test must retrieve a CSV file, named network_devices.csv, located at /home/stauto/ on Server B. The test must parse the CSV data, generating a list of objects. Each object will represent a row from the CSV, with attributes dynamically created based on the CSV header and populated with the corresponding data. A sample network_devices.csv file is provided in this repository, representing a typical file found on Server B.

Rigorous type validation is required during the parsing process, enforcing the following data types: integer for device_id, string for hostname, ipaddress.IPv4Address for ip_address (using the ipaddress library), and string for all other fields, including status, which must be restricted to "online" or "offline". Any invalid entries encountered during parsing should be logged to a file named test_log.log. A requirements.txt file must be provided, specifying all non-standard library dependencies.

The test suite should accept a timeout value, in seconds, via a custom command-line option, --timeout. For example: python my_test.py --timeout=600. During the specified timeout period, the test must periodically, every 20 seconds, check the status of all devices initially parsed as "online" from the CSV file. If any of these initially "online" devices transition to an "offline" state during the timeout period, the test must immediately fail. This status check must be conducted against the live Server B. The submitted code will be evaluated for clarity, readability, adherence to PEP 8, and overall code quality.
