# Flask Blog

A full-featured blogging platform built with Flask, supporting user authentication, rich-text post creation, comments, Gravatar avatars, and contact form email delivery via SendGrid. Deployable to Render with PostgreSQL.

---

## Features

- **User authentication** — register, login, logout with hashed passwords via Werkzeug
- **Role-based access** — admin-only routes for creating, editing, and deleting posts
- **Rich text editor** — CKEditor integration for writing blog posts
- **Comments** — authenticated users can comment on posts
- **Gravatar** — commenter avatars loaded automatically from email
- **Contact form** — sends email via SendGrid API
- **Database** — SQLite for local development, PostgreSQL for production
- **Deployment-ready** — configured for Render with Gunicorn and SSL

---

## Screenshots

![Home page](https://github.com/user-attachments/assets/33d2bc3e-b122-4bc1-a1a4-7182fcbfa600)

![Blog post](https://github.com/user-attachments/assets/17eebd9b-7a2c-49f6-8be8-c4b26fea81a6)

![Contact / About](https://github.com/user-attachments/assets/7a435cc0-dbb0-41c4-af69-e046b0943c55)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flask 2.3.3 |
| Database ORM | Flask-SQLAlchemy 3.1.1 |
| Auth | Flask-Login 0.6.3 |
| Forms | Flask-WTF 1.2.2 + email-validator |
| Rich Text | Flask-CKEditor 1.0.0 |
| UI | Bootstrap-Flask |
| Avatars | Flask-Gravatar 0.5.0 |
| Email | SendGrid |
| Password Hashing | Werkzeug 3.1.1 |
| Production DB | psycopg2-binary (PostgreSQL) |
| WSGI Server | Gunicorn 21.2.0 |

---

## Project Structure

```
.
├── main.py               # App factory, models, and all routes
├── forms.py              # WTForms definitions (Register, Login, Comment, CreatePost)
├── templates/
│   ├── index.html
│   ├── post.html
│   ├── register.html
│   ├── login.html
│   ├── make-post.html
│   ├── about.html
│   └── contact.html
├── static/               # CSS, JS, images
├── requirements.txt
└── .env                  # Local environment variables (not committed)
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

### 2. Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key
DB_URI=sqlite:///posts.db
SENDGRID_API_KEY=your-sendgrid-api-key
FROM_ADD=your-verified-sender@example.com
TO_ADD=your-inbox@example.com
```

### 5. Run the app

```bash
python main.py
```

Visit `http://localhost:5005` in your browser.

---

## Admin Access

The first registered user (ID = 1) is automatically the admin. Only the admin can:

- Create new posts (`/new-post`)
- Edit existing posts (`/edit-post/<id>`)
- Delete posts (`/delete/<id>`)

---

## Deployment (Render)

1. Push your code to GitHub.
2. Create a new **Web Service** on [Render](https://render.com) and connect your repo.
3. Set the **Start Command** to:
   ```
   gunicorn main:app
   ```
4. Add the following **Environment Variables** in Render's dashboard:

   | Key | Value |
   |---|---|
   | `SECRET_KEY` | A long random string |
   | `DB_URI` | Your Render PostgreSQL internal URL |
   | `SENDGRID_API_KEY` | Your SendGrid API key |
   | `FROM_ADD` | Verified sender email |
   | `TO_ADD` | Recipient email for contact form |

5. Render will automatically handle SSL for PostgreSQL connections.

---

## Environment Variables Reference

| Variable | Description | Required |
|---|---|---|
| `SECRET_KEY` | Flask session secret | Yes |
| `DB_URI` | Database connection string | Yes |
| `SENDGRID_API_KEY` | SendGrid API key for email | Yes |
| `FROM_ADD` | Verified sender email address | Yes |
| `TO_ADD` | Contact form recipient address | Yes |

---

## Dependencies

```
Flask==2.3.3
bootstrap-flask
Flask-CKEditor==1.0.0
Flask-Gravatar==0.5.0
Flask-Login==0.6.3
Flask-SQLAlchemy==3.1.1
Flask-WTF==1.2.2
Werkzeug==3.1.1
python-dotenv==1.0.1
psycopg2-binary==2.9.10
gunicorn==21.2.0
Jinja2==3.1.4
MarkupSafe==3.0.2
bleach
email-validator
sendgrid
```

---

## License

MIT
