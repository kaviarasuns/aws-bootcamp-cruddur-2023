# Week 1 — App Containerization

https://code.visualstudio.com/docs/containers/overview

> Gitpod is preinstalled with theis extension

** Containerize Backend

*** Run Python

---sh
cd backend-flask
export FRONTEND_URL="**
export BACKEND_URL="*"
python3 -m flask run--host-0.0.0.0 --port-4567
cd . .
---

- make sure to unlock the port on the port tab
- open the link for 4567 in your browser
- change the url to '/api/activities/home'
- you should get back json



### Build Container

docker build -t backend-flask ./backend-flask


### Run Container

Run 

docker run --rm -p 4567:4567 -it backend-flask

FRONTEND_URL="*" BACKEND_URL="*" docker run --rm -p 4567:4567 -it backend-flask

Run in background

docker container run --rm -p 4567:4567 -d backend-flask
