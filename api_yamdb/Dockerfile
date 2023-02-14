
FROM python:3.7-slim

COPY ./ /app


RUN pip install -r /app/requirements.txt

RUN pip3 install gunicorn && pip install psycopg2-binary

WORKDIR /app/api_yamdb/

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]







