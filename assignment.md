# Create a database for your project

While you may not use a SQL database for your project, we'll practice by creating some tables.

Start with the data model you worked on for your warmup today (warmup.md).

## Easy Mode

Based on what you learned today, update your data model and document it in a file called `data_model.md`.

## Normal Mode

Create at least three tables, with a few fields each, to match your data model.

* Each table should have an `id` column that is `SERIAL PRIMARY KEY`
* Each column should have an appropriate data type
* Create a file called project_tables.sql, and copy the `CREATE TABLE` statements you used to create your tables into it.
* Insert some data into those tables.
* Create a file called project_data.sql, and copy the `INSERT INTO` statements into it.

Save and check both of those files into github.

## Adventure Mode

* Use `ALTER TABLE` to add a column to one of your tables.
* Use `ALTER TABLE` to add default values to your columns as appropriate.
* Use `ALTER TABLE` to add not null constraints to your columns as appropriate.
