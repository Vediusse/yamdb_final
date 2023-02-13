FROM python:3.7-slim

WORKDIR /app

COPY requirements.txt .

RUN pip3 install -r requirements.txt --no-cache-dir

COPY ./ .

RUN pip3 install gunicorn && pip install psycopg2-binary

WORKDIR api_yamdb

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]








