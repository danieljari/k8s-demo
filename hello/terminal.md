docker image build  -t dockerimage .

docker container run -p 9999:8888 dockerimage

went to http://localhost:9999/

