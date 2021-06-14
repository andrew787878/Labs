# Labs
import uuid
import httpx
import json
from fastapi import FastAPI


app = FastAPI()

LOG_HOST = 'http://127.0.0.1:8001/lab2'
MES_HOST = 'http://127.0.0.1:8002/lab2'


@app.post("/lab2", status_code=200)
def message_handler(msg: str):
    httpx.post(LOG_HOST, data=json.dumps({'id': str(uuid.uuid4()), 'msg': msg}))


@app.get("/lab2")
def message_handler():
    log_resp = httpx.get(LOG_HOST)
    mess_resp = httpx.get(MES_HOST)
    return log_resp.text.strip('"') + mess_resp.text.strip('"')
