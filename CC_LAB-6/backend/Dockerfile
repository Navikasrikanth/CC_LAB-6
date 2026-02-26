FROM gcc:latest

WORKDIR /app

COPY app.cpp .

RUN g++ -o app app.cpp

EXPOSE 8081

CMD ["./app"]
