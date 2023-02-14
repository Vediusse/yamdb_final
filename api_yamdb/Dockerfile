FROM python:3.7-slim

WORKDIR /app

COPY requirements.txt .

COPY ./api_yamdb/ .

WORKDIR /api_yamdb

RUN pip3 install -r requirements.txt --no-cache-dir

RUN pip3 install gunicorn && pip install psycopg2-binary

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]




