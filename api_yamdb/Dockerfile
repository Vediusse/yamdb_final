
FROM python:3.7-slim

WORKDIR /app

COPY ./api_yamdb/ .

COPY requirements.txt /tmp/requirements.txt

RUN pip3 install -r /tmp/requirements.txt--no-cache-dir

RUN pip3 install gunicorn && pip install psycopg2-binary

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]







