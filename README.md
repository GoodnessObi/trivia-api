# Trivia API

## Table of contents

- [Setting up the Backend](#setting-up-the-backend)
  - [Install Dependencies](#install-dependencies)
  - [Set up the Database](#set-up-the-database)
  - [Run the Server](#run-the-server)
- [Testing](#testing)
- [Local Development](#local-development)
- [API Documentation](#api-documentation)
  - [Base URL](#base-url)
  - [Error](#error)
  - [Endpoints](#endpoints)


## Setting up the Backend

### Install Dependencies

1. **Python 3.8.10** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createbd trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Run the Server

* Install a virtual environment and activate it
```
python3 -m venv venv
. venv/bin/activate
```

* Run the requirements.txt script to install all needed dependencies
```
pip install requirements.txt
```

* Run the application
To run the server, execute: 
```
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```
These commands put the application in development and directs our application to use the `__init__.py` file in our flaskr folder. Working in development mode shows an interactive debugger in the console and restarts the server whenever changes are made. If running locally on Windows, look for the commands in the [Flask documentation](http://flask.pocoo.org/docs/1.0/tutorial/factory/).

The application is run on `http://127.0.0.1:5000/` by default and is a proxy in the frontend configuration. 

The `--reload` flag will detect file changes and restart the server automatically.

---

## Testing

To deploy the tests, run

```bash
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

Alternatively,

- Create the database and a user<br>
  In your terminal, navigate to the _/trivia-app/backend/_ directory, and run the following:

```bash
cd trivia-app/backend
# Connect to the PostgreSQL
psql postgres
#View all databases
\l
# Create the database, create a user - `student`, grant all privileges to the student
\i setup.sql
# Exit the PostgreSQL prompt
\q
```

- then...

```
psql trivia_test < trivia.psql
python test_flaskr.py
```

---

## Local Development

The instructions below are meant for the local setup.

#### Pre-requisites

- Developers using this project should already have Python3, pip and node installed on their local machines.

- **Start your virtual environment**
  From the backend folder run

```bash
# Mac users
python3 -m venv venv
source venv/bin/activate
# Windows users
> py -3 -m venv venv
> venv\Scripts\activate
```

- **Install dependencies**<br>
  From the backend folder run

```bash
# All required packages are included in the requirements file.
pip3 install -r requirements.txt
```

### Step 0: Start/Stop the PostgreSQL server

Mac users can follow the commands below:

```bash
which postgres
postgres --version
# Start/stop
pg_ctl -D /usr/local/var/postgres start
pg_ctl -D /usr/local/var/postgres stop
```

Linux users can follow the commands below:

```bash
which postgres
postgres --version
# Start/stop
sudo service postgresql start
sudo service postgresql stop
```

### Step 1 - Create and Populate the database

1. **Create the database and a user**<br>
   In your terminal, navigate to the _/trivia-app/backend/_ directory, and run the following:

```bash
cd trivia-app/backend
# Connect to the PostgreSQL
psql postgres
#View all databases
\l
# Create the database, create a user - `student`, grant all privileges to the student
\i setup.sql
# Exit the PostgreSQL prompt
\q
```

2. **Create tables**<br>
   Once your database is created, you can create tables (`categories`) and (`questions`) and apply contraints

```bash
# Mac users
psql -f books.psql -U student -d trivia
# Linux users
su - postgres bash -c "psql trivia < /path/to/exercise/backend/trivia.psql"

```

**You can even drop the database and repopulate it, if needed, using the commands above.**

## API Documentation
The Trivia API is organized around REST. It has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes and verbs.

### Base URL
The application presently runs only locally on: 
```
http://127.0.0.1:5000/
```

### Error
**HTTP Status Code Summary**
| Code | Message            | Summary                                                                                       |
|------|--------------------|-----------------------------------------------------------------------------------------------|
| 200  | ok                 | Everything worked as expected.                                                                |
| 400  | bad request        | The request was unacceptable, often due to missing required parameter.                        |
| 404  | resource not found | The requested resource doesn't exist.                                                         |
| 405  | method not allowed | The request method is not supported                                                           |
| 422  | unprocessable       | The request entity was correct but the server was unable to process the contained information |

**Sample Response**
```json
{
  "error": 404,
  "message": "resource not found",
  "success": false
}
```

### Endpoints

`GET '/categories'`

- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None

**Sample Request**
```
curl http://127.0.0.1:5000/categories
```

- Returns: An object with a single key, `categories`, that contains an object of `id: category_string` key: value pairs.

```json
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true
}
```

---
`GET '/questions?page=${integer}'`

- Fetches a paginated set of questions, a total number of questions, all categories and current category string.
- Request Arguments: `page` - integer

**Sample Request**
```
curl http://127.0.0.1:5000/questions?page=1
```

- Returns: An object with 10 paginated questions, total questions, object including all categories, and current category string

```json
{
  "questions": [
    {
      "id": 1,
      "question": "This is a question",
      "answer": "This is an answer",
      "difficulty": 5,
      "category": 2
    }
  ],
  "totalQuestions": 100,
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "currentCategory": "History"
}
```

---
`GET '/categories/${id}/questions'`

- Fetches questions for a cateogry specified by id request argument
- Request Arguments: `id` - integer

**Sample Request**
```
curl http://127.0.0.1:5000/categories/1/questions
```

- Returns: An object with questions for the specified category, total questions, and current category string


```json
{
  "current_category": "Science",
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "success": true,
  "total_questions": 3
}
```

---

`DELETE '/questions/${id}'`

- Deletes a specified question using the id of the question
- Request Arguments: `id` - integer

**Sample Request**
```
curl -X DELETE http://127.0.0.1:5000/questions/4
```

- Returns: An object with the id of the deleted question, total questions and 10 paginated questions.

```json
{
  "deleted": 4,
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }
  ],
  "success": true,
  "total_questions": 15
}
```

---

`POST '/quizzes'`

- Sends a post request in order to get the next question
- Request Body:

```json
{
  "previous_questions": [1, 4, 20, 15],
  "quiz_category": {
    "type": "Science",
    "id": 1
  },
  "success": true
}
```

**Sample Request**
This will return random questions in Science category.
```
curl -X POST -H "Content-Type: application/json" \
  -d '{"previous_questions":[], "quiz_category":{"type": "Science", "id": 1}}' \
  http://127.0.0.1:5000/quizzes
```

- Returns: a single new question object

```json
{
  "question": {
    "answer": "Alexander Fleming",
    "category": 1,
    "difficulty": 3,
    "id": 21,
    "question": "Who discovered penicillin?"
  },
  "success": true
}
```

---

`POST '/questions'`

- Sends a post request in order to add a new question
- Request Body:

```json
{
  "question": "Heres a new question string",
  "answer": "Heres a new answer string",
  "difficulty": 1,
  "category": 3
}
```

**Sample Request**
This will return random questions in Science category.
```
curl -X POST -H "Content-Type: application/json" \
  -d '{"questions":"Heres a new question string", "answer": "Heres a new answer string", "difficulty": 1,"category": 3}' \
  http://127.0.0.1:5000/questions
```

- Returns: An object with the id of the created question, total questions and 10 paginated questions.

```json
{
  "created": 25,
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "One",
      "category": 2,
      "difficulty": 4,
      "id": 18,
      "question": "How many paintings did Van Gogh sell in his lifetime?"
    }
  ],
  "success": true,
  "total_questions": 16
}
````

---

`POST '/questions'`

- Sends a post request in order to search for a specific question by search term
- Request Body:

```json
{
  "searchTerm": "this is the term the user is looking for"
}
```
**Sample Request**
```
curl -X POST -H "Content-Type: application/json" \
  -d '{"searchTerm": "largest lake"}' \
  http://127.0.0.1:5000/questions/search
```

- Returns: any array of questions, a number of totalQuestions that met the search term and the current category string

```json
{
  "current_category": "History",
  "questions": [
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    }
  ],
  "success": true,
  "total_questions": 1
}
```
