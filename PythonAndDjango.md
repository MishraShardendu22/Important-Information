# Important Django and Virtual Environment Commands

## Setting Up Django Projects

1. **Navigate to Your Desired Directory**:
   ```bash
   cd D:\Coding Stuff Shardendu Mishra\Django
   ```

2. **Create a Virtual Environment**:
   ```bash
   python -m venv myenv
   ```

3. **Activate the Virtual Environment**:
   ```bash
   .\myenv\Scripts\activate  # Windows
   ```

4. **Install Django**:
   ```bash
   pip install django
   ```

5. **Create a New Django Project**:
   ```bash
   django-admin startproject myproject
   ```

6. **Run the Django Development Server**:
   ```bash
   python manage.py runserver
   ```

## Managing Virtual Environments

### Using `venv`
- **Activate Environment**:
  ```bash
  .\myenv\Scripts\activate  # Windows
  ```

- **Deactivate Environment**:
  ```bash
  deactivate
  ```

### Using `virtualenvwrapper` (Optional)
1. **Install virtualenvwrapper-win**:
   ```bash
   pip install virtualenvwrapper-win
   ```

2. **Create a Virtual Environment**:
   ```bash
   mkvirtualenv myenv
   ```

3. **Activate Environment with `workon`**:
   ```bash
   workon myenv
   ```

4. **Deactivate Environment**:
   ```bash
   deactivate
   ```

## Optional Commands

- **Check Installed Django Version**:
  ```bash
  django-admin --version
  ```

- **Create an App Within a Project**:
  ```bash
  python manage.py startapp myapp
  ```

- **Create Migrations for Database Changes**:
  ```bash
  python manage.py makemigrations
  ```

- **Apply Migrations to Database**:
  ```bash
  python manage.py migrate
  ```

- **Create a Superuser for Admin Panel**:
  ```bash
  python manage.py createsuperuser
  ```

- **Run the Shell for Testing Models/Queries**:
  ```bash
  python manage.py shell
  
