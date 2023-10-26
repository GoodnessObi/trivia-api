# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.8.10** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

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

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
flask run --reload
```

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
