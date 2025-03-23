# Gemini Powered Tutor

## Overview

Gemini Powered Tutor is an AI-driven web application designed to assist users by providing intelligent and accurate responses to their questions. Leveraging the power of the Gemini API, this project integrates a Django backend with a React frontend to create a seamless and interactive tutoring experience. Users can ask questions through a chat interface, and the system delivers real-time answers, making it an ideal tool for learning and exploration.

### Features
- **Interactive Chat Interface**: A user-friendly chat window built with React and Framer Motion for smooth animations.
- **Gemini API Integration**: Utilizes the Gemini API to generate intelligent responses to user queries.
- **Real-Time Responses**: Provides instant answers to questions with minimal latency.
- **CORS Support**: Configured with `django-cors-headers` for secure cross-origin communication between the frontend and backend.
- **Scalable Architecture**: Built with Django for the backend and React for the frontend, ensuring modularity and scalability.

## Tech Stack
- **Backend**: Python, Django
- **Frontend**: React, Framer Motion
- **API**: Gemini API
- **CORS**: `django-cors-headers` for cross-origin resource sharing
- **Development Tools**: npm, Git

## Prerequisites
Before setting up the project, ensure you have the following installed:
- Python 3.8 or higher
- Node.js and npm
- Git
- A Gemini API key (you can obtain one from the Google Cloud Console)

## Setup Instructions

### 1. Clone the Repository
Clone the project repository to your local machine:
```bash
git clone https://github.com/regvedpande/geminipoweredtutor.git
cd geminipoweredtutor
```

### 2. Set Up the Backend (Django)
1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   .\venv\Scripts\activate  # On Windows
   source venv/bin/activate  # On macOS/Linux
   ```
3. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```
   *Note*: If `requirements.txt` is not present, install the following packages manually:
   ```bash
   pip install django django-cors-headers requests
   ```
4. Configure the Gemini API Key:
   - Open `api/views.py` and replace the placeholder API key with your Gemini API key:
     ```python
     api_key = "YOUR_GEMINI_API_KEY"
     ```
   - For better security, consider using environment variables:
     ```python
     import os
     api_key = os.getenv("GEMINI_API_KEY")
     ```
     Then set the environment variable in your system or in a `.env` file using `python-dotenv`.
5. Update CORS settings in `tutor/settings.py`:
   Ensure the following is configured to allow the frontend origin:
   ```python
   INSTALLED_APPS = [
       ...
       'corsheaders',
       ...
   ]

   MIDDLEWARE = [
       'corsheaders.middleware.CorsMiddleware',
       'django.middleware.common.CommonMiddleware',
       ...
   ]

   CORS_ALLOWED_ORIGINS = [
       "http://localhost:3002",  # Update to match your frontend port
   ]
   ```
6. Run the Django development server:
   ```bash
   python manage.py runserver 3001
   ```
   The backend should now be running on `http://localhost:3001`.

### 3. Set Up the Frontend (React)
1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```
2. Install the required npm packages:
   ```bash
   npm install
   ```
3. Update the backend URL in `src/ChatWindow.js`:
   Ensure the `fetch` call points to the correct backend port (3001):
   ```javascript
   const response = await fetch('http://localhost:3001/api/ask/', {
       method: 'POST',
       headers: {
           'Content-Type': 'application/json',
       },
       body: JSON.stringify({ question }),
   });
   ```
4. Run the React development server on port 3002:
   - Update the `start` script in `package.json` to use port 3002:
     ```json
     "start": "PORT=3002 react-scripts start"
     ```
   - Alternatively, create a `.env` file in the `frontend` directory:
     ```bash
     echo PORT=3002 > .env
     ```
   - Start the frontend:
     ```bash
     npm start
     ```
   The frontend should now be running on `http://localhost:3002`.

### 4. Test the Application
1. Open your browser and go to `http://localhost:3002`.
2. Ask a question in the chat window, such as "What is the capital of Canada?"
3. The system should respond with: "The capital of Canada is Ottawa."

## Usage
- **Ask Questions**: Type your question in the input field and press "Send" to receive a response from the Gemini API.
- **View Responses**: Responses are displayed in the chat window with a "tutor" label.
- **Error Handling**: If the backend is unreachable, the frontend will display an error message like "Failed to connect to the server: Failed to fetch."

## Troubleshooting
- **Backend Not Responding**:
  - Ensure the Django server is running on port 3001.
  - Check the terminal for any error messages.
  - Verify the Gemini API key is correct and has the necessary permissions.
- **CORS Issues**:
  - Confirm that `CORS_ALLOWED_ORIGINS` in `tutor/settings.py` includes `http://localhost:3002`.
  - Restart the Django server after making changes.
- **Frontend Not Loading**:
  - Ensure the React server is running on port 3002.
  - Check the browser console (F12) for any errors.
- **Firewall/Antivirus Blocking**:
  - Temporarily disable your firewall or antivirus and test the connection.
  - Add exceptions for ports 3001 and 3002 in your firewall/antivirus settings.

## Contributing
Contributions are welcome! If you’d like to contribute to Gemini Powered Tutor, please follow these steps:
1. Fork the repository.
2. Create a new branch for your feature or bug fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes and commit them:
   ```bash
   git commit -m "Add your commit message"
   ```
4. Push your changes to your fork:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a pull request on the main repository.

## Contact
For questions, suggestions, or issues, please reach out to:  
📧 **regregd?@outlook.com**

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

