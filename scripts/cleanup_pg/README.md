# Open WebUI Cleanup (PG/pgvector)

## Description
This script allows to cleanup an Open WebUI deployment by pruning old chats and then all unused files and vector collections that are not referenced anymore in the system. It performs cleanup operations on both the main database and the vector database, as well as the filesystem. This variant works for deployments using PostgreSQL for both databases, with pgvector extension for the vector DB.

Although this is safe to use with the correct parameters and a current (0.6.5) Open WebUI, **please** be careful when using this program and test it in a safe environment before deploying it to production. Always run a `--dry-run` first to make sure the amount of deleted elements is in the expected range.

Also, please verify yourself that it is still up to date and compatible with current Open WebUI releases.

## Features
- **Cleanup Old Chats**: Deletes chats that are older than a specified number of days.
- **Delete Unused Files**: Removes files that are not referenced in the chat or knowledge tables.
- **Delete Unused Collections**: Removes collections that are not referenced in the chat, file, or memory tables.
- **Filesystem Cleanup**: Deletes files from the uploads directory that are not referenced in the database.

## Requirements
- Python 3.x
- `psycopg` library (`pip install psycopg`) (must be 3.x)
- Access to the main and vector databases
- Access to the uploads directory

## Usage
1. **Install Dependencies**
   For example:
   ```bash
   pip install psycopg
   ```

2. **Run the Script**
   The script can be executed from the command line with the following parameters:
   ```bash
   python cleanup_pg.py --main-db-url <main_db_url> --vector-db-url <vector_db_url> --uploads-dir <uploads_dir> --keep-days <keep_days> [--dry-run] [--verbose] [--debug]
   ```

   - `--main-db-url`: Database URL for the main database.
   - `--vector-db-url`: Database URL for the vector database.
   - `--uploads-dir`: Path to the uploads directory.
   - `--keep-days`: Number of days to keep chats.
   - `--dry-run`: Perform a dry run without making any changes.
   - `--verbose`: Enable verbose output.
   - `--debug`: Enable debug mode (implies `--dry-run` and extra verbose output).

## Example
```bash
python cleanup_pg.py --main-db-url "postgresql://user:password@localhost/main_db" --vector-db-url "postgresql://user:password@localhost/vector_db" --uploads-dir "/path/to/uploads" --keep-days 30 --verbose
```

## Logging
The script logs errors at the ERROR level by default and additional information at the INFO and DEBUG levels if enabled.
