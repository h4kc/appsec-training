### Static layers
FROM alpine:3.7

# Installing needed binaries and deps. Then removing unneeded deps:
RUN apk update --no-cache && apk add nodejs nodejs-npm bash git dos2unix

### Dynamic layers
RUN addgroup -g 1000 app 
RUN adduser -u 1000 -G app -D -h /home/app app

COPY ./ /home/app/CMD4

# Switching to the new app location:
WORKDIR /home/app/CMD4

RUN chown -R app:app /home/app/CMD4

# Switching to the limited user


# Installing needed binaries and deps:
RUN npm install --silent

# Fixing Windows line endings for our students:
RUN find . -name "*.sh" -o -name "*.py" -o -name "*.css" -o -name "*.js" | xargs dos2unix

# Setting chmod +x on the scripts:
RUN find . -name "*.sh" -o -name "*.py" | xargs chmod +x

# Starting the actual application:
ENTRYPOINT ["node", "./app.js"]