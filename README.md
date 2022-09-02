# Trivia App Project

This is a project given by ALX-T Full Stack Developer - Udacity. The task given was to build the API of the trivia app so that people can start holding trivia and see who's the most knowledgeable of the bunch. The application:

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

## Getting Started

[Fork](https://help.github.com/en/articles/fork-a-repo) the project repository and [clone](https://help.github.com/en/articles/cloning-a-repository) your forked repository to your machine. Work on the project locally and make sure to push all your changes to the remote repository.

### Pre-requisites and Local Development

Developers using this project should already have Python3, pip and node installed on their local machines.

#### Backend

From the backend folder run `pip install requirements.txt`. All required packages are included in the requirements file.

To run the application run the following commands:

```
FLASK_APP=flaskr FLASK_DEBUG=True flask run
```

These commands put the application in development and directs our application to use the `__init__.py` file in our flaskr folder.

The application is run on `http://127.0.0.1:5000/` by default and is a proxy in the frontend configuration.

#### Frontend

The frontend directory contains a complete React frontend to consume the data from the Flask server.

From the frontend folder, run the following commands to start the client:

```
npm install // only once to install dependencies
npm start
```

By default, the frontend will run on localhost:3000.

### Tests

In order to run tests navigate to the backend folder and run the following commands:

```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

The first time you run the tests, omit the dropdb command.

## API Reference

### Getting Started

- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration.
- Authentication: This version of the application does not require authentication or API keys

### Error Handling

Errors are returned as JSON objects in the following format:

```
{
    "success": False,
    "error": 400,
    "message": "bad request"
}
```

The API will return five error types when requests fail:

- 400: Bad Request
- 404: Resource Not Found
- 405: Method Not Allowed
- 422: Unprocessable
- 500: Server Error

### Endpoints

#### GET '/categories'

- General:
  - Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
  - Returns: An object with a single key, categories, that contains an object of id: category_string key: value pairs and also the success value
- Sample: `curl http://127.0.0.1:5000/categories`

```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true,
  "totalCategories": 6
}
```

#### GET '/questions?page=${integer}'

- General:
  - Fetches a paginated set of questions, a total number of questions and all categories
  - Returns: An object with 10 paginated questions, total questions, object including all categories and a success value
- Sample: `curl http://127.0.0.1:5000/questions?page=1`

```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Tom Cruise",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Edward Scissorhands",
      "category": 5,
      "difficulty": 3,
      "id": 6,
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    },
    {
      "answer": "Muhammad Ali",
      "category": 4,
      "difficulty": 1,
      "id": 9,
      "question": "What boxer's original name is Cassius Clay?"
    },
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": 6,
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    },
    {
      "answer": "George Washington Carver",
      "category": 4,
      "difficulty": 2,
      "id": 12,
      "question": "Who invented Peanut Butter?"
    },
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "Agra",
      "category": 3,
      "difficulty": 2,
      "id": 15,
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ],
  "success": true,
  "totalQuestions": 20
}
```

#### DELETE '/questions/${id}'

- General:
  - Deletes a specified question using the id of the question
  - Returns: The id of the question and a success value
- Sample: `curl -X DELETE http://127.0.0.1:5000/questions/12`

```
{
  "success": True,
  "deleted": question_id,
}
```

#### POST '/questions'

- General:

  - Sends a post request in order to add a new question
  - Returns: The id of the created question, success value, total books, and

- Sample: `curl -X POST -H "Content-Type: application/json" -d '{"question":"Who is the winner of UCL 2021/22 season", "answer":"Real Madrid", "category":"6", "difficulty":"2}' http://127.0.0.1:5000/questions`

```
{
  "created": 25,
  "question": [
    {
    "answer": "Real Madrid",
    "category": 6,
    "difficulty": 2,
    "id": 25,
    "question": "Who is the winner of UCL 2021/22 season"
    }
  ],
  "success": true,
  "totalQuestions": 20
}
```

#### POST '/questions/search'

- General:
  - Sends a post request in order to search for a specific question by search term
  - Returns: any array of questions, a number of totalQuestions that met the search term and success value
- Sample: `curl -X POST -H "Content-Type: application/json" -d '{"searchTerm":"title"}' http://127.0.0.1:5000/questions/search `

```
{
  "questions": [
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Edward Scissorhands",
      "category": 5,
      "difficulty": 3,
      "id": 6,
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }
  ],
  "success": true,
  "totalQuestions": 20
}
```

#### GET '/categories/${id}/questions'

- General:
  - Fetches questions for a cateogry specified by id request argument
  - Returns: An object with questions for the specified category, total questions current category string and also success value
- Sample: `curl http://127.0.0.1:5000/categories/6/questions`

```
{
  "currentCategory": "Sports",
  "questions": [
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": 6,
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    },
    {
      "answer": "Real Madrid",
      "category": 6,
      "difficulty": 2,
      "id": 25,
      "question": "Who is the winner of UCL 2021/22 season"
    }
  ],
  "success": true,
  "totalQuestions": 20
}
```

#### POST '/quizzes'

- General:
  - Sends a post request in order to get the next question
  - Allows the user to play the quiz either by selecting all or by category
  - Returns: a single new question object and success value
  - If all questions for a particular category is exhausted null object is returned for question thereby ending the quiz
- Sample: `curl -X POST 'http://127.0.0.1:5000/quizzes' -H 'Content-Type: application/json' -d '{"previous_questions": [20, 21], "quiz_category":{"id":"1", "type":"Science"}}'`

```
{
  "question": {
    "answer": "Blood",
    "category": 1,
    "difficulty": 4,
    "id": 22,
    "question": "Hematology is a branch of medicine involving the study of what?"
  },
  "success": true
}
```
