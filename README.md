```markdown
# Flask User Registration and Query App

This Flask application implements user registration, login, and text/voice query handling. It integrates OpenAI's GPT for processing queries and uses SpeechRecognition for voice input and pyttsx3 for text-to-speech conversion.

## Features

- **User Registration and Login**: Register users with email and password, log them in, and manage sessions.
- **Text Queries**: Process text-based queries using OpenAI's GPT model.
- **Voice Queries**: Allow users to ask queries via voice input and get spoken responses.
- **Database**: SQLite database for storing user credentials.

## Requirements

Make sure to have Python 3.x installed. Install the necessary Python packages via `pip` using the provided `requirements.txt`.

### Install Dependencies

1. Clone this repository or download the code.
2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```
3. Activate the virtual environment:
   - For **Windows**:
     ```bash
     venv\Scripts\activate
     ```
   - For **Mac/Linux**:
     ```bash
     source venv/bin/activate
     ```
4. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### `requirements.txt`:
```txt
Flask
Flask-SQLAlchemy
Flask-Bcrypt
Flask-Login
SpeechRecognition
pyttsx3
openai
requests
```

## Setup

### Configure OpenAI API Key

To use OpenAI’s GPT, you need an API key. Set the `OPENAI_API_KEY` environment variable in your terminal or add it directly to the code.

To set the environment variable in **Linux/Mac**:
```bash
export OPENAI_API_KEY="your_openai_api_key"
```

For **Windows**, you can use:
```bash
set OPENAI_API_KEY="your_openai_api_key"
```

### Initialize the Database

The app uses SQLite for the user database. The database will be automatically created when the application runs. However, you can manually create the tables using Flask commands if necessary:
```bash
flask db init
flask db migrate
flask db upgrade
```

## Running the Application

To start the Flask application, run the following command:

```bash
python app.py
```

The app will be hosted on `http://127.0.0.1:5000/`.

### Endpoints:

- **POST `/register`**: Register a new user.
  - **Request JSON body**:
    ```json
    {
      "username": "testuser",
      "email": "test@example.com",
      "password": "password"
    }
    ```
  - **Response**:
    ```json
    {
      "message": "User registered successfully"
    }
    ```

- **POST `/login`**: Log in a registered user.
  - **Request JSON body**:
    ```json
    {
      "email": "test@example.com",
      "password": "password"
    }
    ```
  - **Response**:
    ```json
    {
      "message": "Login successful"
    }
    ```

- **GET `/logout`**: Log out the current user. Requires user to be logged in.
  - **Response**:
    ```json
    {
      "message": "Logged out successfully"
    }
    ```

- **POST `/query`**: Process a text query with OpenAI's GPT.
  - **Request JSON body**:
    ```json
    {
      "query": "What's the weather like today?"
    }
    ```
  - **Response**:
    ```json
    {
      "response": "It's sunny and warm today."
    }
    ```

- **POST `/voice_query`**: Process a voice query and provide a spoken response.
  - This endpoint listens to the user's microphone for input and returns a spoken response.
  - **Response**:
    ```json
    {
      "response": "It's sunny and warm today."
    }
    ```

## Testing the Application

To test the application, the script includes an auto-test of the user registration, login, and logout functionality. You can run the tests by executing the following block in your terminal or adding it to the code:

```python
print("Testing user registration and login")
with app.test_client() as client:
    response = client.post('/register', json={'username': 'testuser', 'email': 'test@example.com', 'password': 'password'})
    print(response.get_json())
    response = client.post('/login', json={'email': 'test@example.com', 'password': 'password'})
    print(response.get_json())
    response = client.get('/logout')
    print(response.get_json())
```

## Troubleshooting

- **Microphone issues with SpeechRecognition**: Ensure `PyAudio` is installed. You can install it via:
  ```bash
  pip install pyaudio
  ```
  
- **OpenAI API key errors**: Make sure your OpenAI API key is set up correctly in the environment variables or directly in the code.

- **Database errors**: If the database doesn't appear, try running the Flask migrations or ensure the app is able to access the database file.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Feel free to modify and extend the application to fit your needs.
```

### How to Use:
1. **Clone the repository or download the code.**
2. **Set up the environment as described in the `Install Dependencies` section.**
3. **Configure OpenAI API Key for the voice and text query features.**
4. **Run the app using `python app.py`.**
5. **Use a tool like Postman or Curl to test the different endpoints or test via the browser (for login/logout).**
