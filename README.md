# RULE ENGINE WITH AST

A simple 3-tier rule engine application(Simple UI, API and Backend, Data) to determine user eligibility based on attributes like age, department, income, spend etc.The system uses Abstract Syntax Tree (AST) to represent conditional rules and allow for dynamic creation,combination, and modification of these rules.


## Install the required libraries
1.
   ```bash
   pip install -r requirements.txt

## Run the Flask application:

2.
   ```bash
   python main.py

## 3 Tier Rule Engine Application details:

1. Backend Code - main.py 
2. Frontend Code - ruleeng.py
3. Test Code - test.py

## Data Structure:

1. Defined a data structure to represent the AST.
2. The data structure should allow rule changes
3. E,g One data structure could be Node with following fields
      1. type: String indicating the node type ("operator" for AND/OR, "operand" for
conditions)
      2. left: Reference to another Node (left child)
      3. right: Reference to another Node (right child for operators)
      4. value: Optional value for operand nodes (e.g., number for comparisons)

## Data Storage:

1. Defined the choice of database for storing the above rules and application metadata
2. Defined the schema with samples.

## Sample Rules:

1. rule1 = "((age > 30 AND department = 'Sales') OR (age < 25 AND
department = 'Marketing')) AND (salary > 50000 OR experience >
5)"
2. rule2 = "((age > 30 AND department = 'Marketing')) AND (salary >
20000 OR experience > 5)"


## API Design:

1. create_rule(rule_string): This function takes a string representing a rule (as
shown in the examples) and returns a Node object representing the corresponding AST.

3. combine_rules(rules): This function takes a list of rule strings and combines them
into a single AST. It should consider efficiency and minimize redundant checks. You can
explore different strategies (e.g., most frequent operator heuristic). The function should
return the root node of the combined AST.

4. evaluate_rule(JSON data): This function takes a JSON representing the combined
rule's AST and a dictionary data containing attributes (e.g., data = {"age": 35,
"department": "Sales", "salary": 60000, "experience": 3}). The
function should evaluate the rule against the provided data and return True if the user is
of that cohort based on the rule, False otherwise.

## Test Cases:

1. Created individual rules from the examples using create_rule and verified their AST
representation.
2. Combined the example rules using combine_rules and ensured the resulting AST
reflects the combined logic.
3. Implemented sample JSON data and test evaluate_rule for different scenarios.
4. Explored combining additional rules and tested the functionality.

## API Endpoints - Check in PostMan:

1. POST Request: http://127.0.0.1:5000/create_rule
    ```json
    { "rule_string": "(age > 30 AND department = 'Sales') OR (salary > 50000)" }

2. POST Request: http://127.0.0.1:5000/modify_rule
     ```json
     { "rule_id": 1, "new_rule_string": "age > 40 AND department = 'HR'" }

3. POST Request: http://127.0.0.1:5000/combine_rules
      ```json
      { "rule_ids": [1, 2] }

4. POST Request: http://127.0.0.1:5000/evaluate_rule
   ```json
   { "rule_id": 3, "data": { "age": 35, "department": "Sales", "salary": 60000, "experience": 6 } }


## Checking the working of Application:

  1. Frontend:
       ```bash
       python ruleeng.py

  2. Backend:
        ```bash
        python main.py

  3. Testing:
        ```bash
        python test.py

If the application runs successfully it will automatically create data.db database which stores the created rules.

