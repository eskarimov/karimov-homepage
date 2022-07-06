+++
date = 2022-07-04
isPopular = false
tags = ["data engineering", "dbt", "sqlfluff"]
thumbnailPath = "/self/img/thumbs/laptop-tech.jpg" #TODO find a good pic
title = "Combining dbt and SQLFluff"
+++

In this post I'd like to share how to adopt two very useful tools [SQLFluff](https://www.sqlfluff.com/), a SQL linter,
and [dbt](https://www.getdbt.com/), a data modelling tool, into a powerful combination and make it work with pre-commit to ensure all your
SQLs are properly formatted.

Why to combine them at all?
There are a lot of ways to write SQL: leading/trailing commas, lower-upper case of keywords, 
aliasing table and column names, etc.

Since every data engineer and analyst spends a lot of time reading SQL code, 
having a standard style helps to improve this process and also makes writing less error-prone.

dbt is a powerful data modelling tool helping to write less boilerplate code with Jinja templates and 
it has a remarkable ecosystem of different plugins.

Let's have a look at the example, say we have the following SQL:
```sql
SELECT
  order_id,
  ORDER_DATE AS order_date
  , order_price *0.9 AS discounted_price
from orders
```

Doesn't look very reader-friendly, does it?  
Now I'm going to install sqlfluff with pip and create a configuration file for it.  
In this example I'll be using BigQuery as a query engine, so you might need to adjust my code for your setup, 
as well as to enforce certain rules ([reference](https://docs.sqlfluff.com/en/stable/rules.html)):

Installing sqlfluff, dbt and dependent packages:
```shell
pip install sqlfluff
pip install dbt-core
pip install dbt-bigquery
pip install sqlfluff-templater-dbt
```

How my `sqlfliff` looks like:
```ini
[sqlfluff]
verbose = 1
dialect = bigquery
templater = dbt
recurse = 0
runaway_limit = 10
ignore_templated_areas = True
encoding = autodetect
processes = 4

# NB: This config will only apply in the root folder.
sql_file_exts = .sql
    
[sqlfluff:indentation]
indented_joins = False
indented_using_on = False
template_blocks_indent = True
    
[sqlfluff:templater]
unwrap_wrapped_queries = True
    
[sqlfluff:templater:dbt]
profiles_dir = profiles/
profile = bigquery
target = prod
    
[sqlfluff:templater:jinja]
apply_dbt_builtins = True
    
[sqlfluff:rules]
tab_space_size = 4
max_line_length = 110
indent_unit = space
comma_style = leading
allow_scalar = True
single_table_references = consistent
unquoted_identifiers_policy = all
```

Also we need to ignore certain dbt folders by adding them into `.sqlfluffignore`:
```
target/
dbt_modules/
logs/
```

After running `sqlfluff fix` we get:
```sql
SELECT
    order_id
    , order_date AS order_date
    , order_price * 0.9 AS discounted_price
FROM orders
```

Integration with pre-commit hooks works following:
- [Setup pre-commit](https://pre-commit.com/) for your repo.
- Add the hooks into `.pre-commit-config.yaml` as follows:
```yaml
  - repo: https://github.com/sqlfluff/sqlfluff
    rev: 1.1.0
    hooks:
      - id: sqlfluff-fix
        additional_dependencies: ['dbt-core==1.1.0', 'dbt-bigquery==1.1.0', 'sqlfluff-templater-dbt==1.1.0']
        files: |
          models/|
          tests/
      - id: sqlfluff-lint
        additional_dependencies: ['dbt-core==1.1.0', 'dbt-bigquery==1.1.0', 'sqlfluff-templater-dbt==1.1.0']
        files: |
          models/|
          tests/
```
Enjoy!  
Now everytime you want to commit a new change in your dbt models, sqlfluff will try to fix it automatically for you.  
Additionally you can integrate this check with Github Actions or other CI/CD tools and require `sqlfluff lint` to pass
before making merging a new code into the main branch.
