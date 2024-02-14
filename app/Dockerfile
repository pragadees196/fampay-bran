FROM python:3.12-alpine

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
WORKDIR /app

RUN apk --no-cache add curl
COPY poetry.lock pyproject.toml /app/
RUN curl -sSL https://install.python-poetry.org | python3.12 -
RUN /root/.local/bin/poetry install

COPY . .
RUN cd backend
RUN /root/.local/bin/poetry run python backend/manage.py migrate
EXPOSE 8000
CMD ["/root/.local/bin/poetry", "run", "python", "backend/manage.py", "runserver", "0.0.0.0:8000"]
