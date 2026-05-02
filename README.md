# Book Appointment Application

A simple, beautiful appointment booking web app built with Java Servlets, HTML, CSS, and JavaScript.

## Build
\`\`\`bash
mvn clean package
\`\`\`
The WAR file will be in `target/book-appointment.war`.

## Local Run
Copy the WAR to `$TOMCAT_HOME/webapps/` and start Tomcat.
Visit: `http://localhost:8080/book-appointment/`

## CI/CD
- Push to GitHub
- Jenkins pulls the repo, builds via Maven, deploys to Tomcat