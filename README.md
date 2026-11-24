# DevOps & Automation Lab

---

## 1. Pipelines

### Create a simple pipeline using Jenkins.
**Job Name:** `SimplePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'echo Building Application'
            }
        }
        stage('Test') {
            steps {
                bat 'echo Testing Application'
            }
        }
    }
}
```

---

### Create a workspace file handling pipeline using Jenkins.
**Job Name:** `FilePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Create File') {
            steps {
                writeFile file: 'pipeline.txt', text: 'Created by Jenkins Pipeline'
            }
        }
        stage('Show File') {
            steps {
                echo readFile('pipeline.txt')
            }
        }
    }
}
```

---

### Implement a parameterized pipeline using Jenkins.
**Job Name:** `ParameterPipeline`  
**Program:**
```groovy
pipeline {
    agent any
    parameters {
        string(name: 'USERNAME', defaultValue: 'Student', description: 'Enter your name')
    }
    stages {
        stage('Greet') {
            steps {
                echo "Hello, ${params.USERNAME}!"
            }
        }
    }
}
```

---

### Implement a scheduled pipeline using Jenkins.
**Job Name:** `ScheduledPipeline`  
**Program:**
```groovy
pipeline {
    agent any
    triggers {
        cron('H/5 * * * *')
    }
    stages {
        stage('Show Time') {
            steps {
                bat 'echo Build time: %date% %time%'
            }
        }
    }
}
```

---

### Implement a multi-stage pipeline using Jenkins.
**Job Name:** `MultiStagePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'echo Build Completed'
            }
        }
        stage('Test') {
            steps {
                bat 'echo Test Completed'
            }
        }
        stage('Deploy') {
            steps {
                bat 'echo Deploy Completed'
            }
        }
    }
}
```

---

## 2. Freestyle Projects

### Demonstrate file creation and copying using a Jenkins Freestyle Project.
**Job Name:** `FileCopy`  
**Commands:**
```cmd
echo Hello Jenkins > file1.txt
copy file1.txt file2.txt
type file2.txt
```

---

### Demonstrate Continuous Integration and Continuous Development using Jenkins.
**Job Name:** `CIProject`  
**Commands:**
```cmd
echo Starting CI Process
if not exist registration.html exit /b 1
echo Registration Form Verified
echo Build Successful
```

---

### Create a simple Hello World Freestyle Project and demonstrate workspace variables using Jenkins.
**Job Name:** `HelloWorld`  
**Commands:**
```cmd
echo Hello World
echo Job Name: %JOB_NAME%
echo Workspace: %WORKSPACE%
echo Build Number: %BUILD_NUMBER%
```

---

### Create a parameterized Freestyle Project using Jenkins.
**Job Name:** `ParameterizedFreestyle`  
**Commands:**
```cmd
echo Hello %NAME%
```

---

### Create a scheduled Freestyle Project using Jenkins.
**Job Name:** `ScheduledFreestyle`  
**Commands:**
```cmd
echo Scheduled Freestyle Job Running
```

---

## 3. Git Branching

### Create a Git Branching Story Project – "A Tale in Branches" using Git branches, where each branch represents a chapter, and finally merge all chapters into a single book.html file.
**Folder:** `StoryProject`  
**Filename:** `book.html`  

**Commands:**
```bash
# Step 1: Create project & initial book
mkdir StoryProject
cd StoryProject
git init
git branch -M main

# Create book.html:
# <html><body><h1>A Tale in Branches</h1></body></html>

git add book.html
git commit -m "Created book"

# Step 2: Create Chapter 1 branch
git switch -c chapter1

# Add to book.html:
# <h2>Chapter 1</h2><p>A boy started his journey.</p>

git add book.html
git commit -m "Added chapter 1"
git switch main
git merge chapter1

# Step 3: Create Chapter 2 branch
git switch -c chapter2

# Add to book.html:
# <h2>Chapter 2</h2><p>He reached a beautiful village.</p>

git add book.html
git commit -m "Added chapter 2"
git switch main
git merge chapter2
```

**Final book.html:**
```html
<html>
<body>
<h1>A Tale in Branches</h1>

<h2>Chapter 1</h2>
<p>A boy started his journey.</p>

<h2>Chapter 2</h2>
<p>He reached a beautiful village.</p>
</body>
</html>
```

---

## 4. Docker

### Create a simple containerized application using Docker.
**Folder:** `DockerHTML`  

**File 1: index.html**
```html
<!DOCTYPE html>
<html>
<body>
    <h1>Hello Docker</h1>
    <p>My First Containerized Application</p>
</body>
</html>
```

**File 2: Dockerfile**
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Commands:**
```cmd
docker build -t myweb .
docker run -d --name mywebcontainer -p 8082:80 myweb
```

---

### Run a Python file using Docker.
**Folder:** `DockerPython`  

**File 1: hello.py**
```python
print("Hello Python from Docker")
```

**File 2: Dockerfile**
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY hello.py .
CMD ["python", "hello.py"]
```

**Commands:**
```cmd
docker build -t pythonapp .
docker run --rm pythonapp
```

---

### Run a Java file using Docker.
**Folder:** `DockerJava`  

**File 1: Hello.java**
```java
class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Java from Docker");
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Hello.java .
RUN javac Hello.java
CMD ["java", "Hello"]
```

**Commands:**
```cmd
docker build -t javaapp .
docker run --rm javaapp
```

---

### Implement a parameterized constructor in Java using Docker.
**Folder:** `DockerConstructor`  

**File 1: Student.java**
```java
class Student {
    String name;
    int age;

    Student(String n, int a) {
        name = n;
        age = a;
    }

    public static void main(String[] args) {
        Student s = new Student("Sreethan", 20);
        System.out.println("Name: " + s.name);
        System.out.println("Age: " + s.age);
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Student.java .
RUN javac Student.java
CMD ["java", "Student"]
```

**Commands:**
```cmd
docker build -t constructorapp .
docker run --rm constructorapp
```

---

### Implement a palindrome program in Java using Docker.
**Folder:** `DockerPalindrome`  

**File 1: Palindrome.java**
```java
import java.util.Scanner;

class Palindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number: ");
        int n = sc.nextInt();
        int temp = n, rev = 0;

        while (n > 0) {
            rev = rev * 10 + n % 10;
            n = n / 10;
        }

        if (temp == rev)
            System.out.println("Palindrome");
        else
            System.out.println("Not Palindrome");
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Palindrome.java .
RUN javac Palindrome.java
CMD ["java", "Palindrome"]
```

**Commands:**
```cmd
docker build -t palindromeapp .
docker run -it --rm palindromeapp
```

---

### Implement single inheritance in Java using Docker.
**Folder:** `DockerInheritance`  

**File 1: Inheritance.java**
```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

class Inheritance {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.bark();
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Inheritance.java .
RUN javac Inheritance.java
CMD ["java", "Inheritance"]
```

**Commands:**
```cmd
docker build -t inheritanceapp .
docker run --rm inheritanceapp
```

---

## 5. Kubernetes

### Integrate Kubernetes with Docker.
**Folder:** `DockerHTML`  
**Filename:** `deployment.yaml`  

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myweb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myweb
  template:
    metadata:
      labels:
        app: myweb
    spec:
      containers:
        - name: myweb
          image: myweb:latest
          imagePullPolicy: Never
          ports:
            - containerPort: 80
```

**Commands:**
```cmd
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
```

---

### Automate the execution of a containerized application using Kubernetes.
**Folder:** `DockerHTML`  
**Filename:** `service.yaml`  

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myweb-service
spec:
  selector:
    app: myweb
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP
```

**Commands:**
```cmd
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
kubectl get services
kubectl port-forward service/myweb-service 8083:80
```

---

## 6. Selenium Testing

### Write a simple JavaScript program to perform testing using Selenium.
**Folder:** `C:\selenium`  

**File 1: index.html**
```html
<html>
<body>
    <h2>JavaScript Testing</h2>

    <button id="btn" onclick="show()">Click Me</button>

    <p id="msg"></p>

    <script>
        function show() {
            document.getElementById("msg").innerHTML = "Hello World";
        }
    </script>
</body>
</html>
```

**File 2: JavaScriptTest.java**
```java
import org.openqa.selenium.*;
import org.openqa.selenium.edge.EdgeDriver;

public class JavaScriptTest {
    public static void main(String[] args) {
        WebDriver driver = new EdgeDriver();

        driver.get("file:///C:/selenium/index.html");

        JavascriptExecutor js = (JavascriptExecutor) driver;

        js.executeScript("document.getElementById('btn').click()");

        System.out.println(driver.findElement(By.id("msg")).getText());
    }
}
```

**Execution Steps:**
1. Save `index.html` in `C:\selenium`.
2. Create `JavaScriptTest.java` in NetBeans.
3. Add Selenium libraries.
4. Right-click the Java file ➔ Run File.

---

### Develop test cases for a containerized application using Selenium.
**Folder:** `RegistrationApp`  

**File 1: registration.html**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Event Registration</title>
</head>
<body>
    <h2>Event Registration Form</h2>

    <form id="regForm">
        Name: <input type="text" id="name" required><br><br>

        Email: <input type="email" id="email" required><br><br>

        Phone: <input type="text" id="phone" required><br><br>

        Gender:
        <select id="gender" required>
            <option value="">Select</option>
            <option>Male</option>
            <option>Female</option>
            <option>Other</option>
        </select><br><br>

        Event:
        <select id="event" required>
            <option value="">Select</option>
            <option>Hackathon</option>
            <option>Workshop</option>
        </select><br><br>

        <button type="submit">Register</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("regForm").onsubmit = function(e) {
            e.preventDefault();
            document.getElementById("message").innerText =
                "Registration Successful!";
        };
    </script>
</body>
</html>
```

**File 2: Dockerfile**
```dockerfile
FROM nginx:alpine
COPY registration.html /usr/share/nginx/html/index.html
```

**File 3: RegistrationTest.java**
```java
import org.openqa.selenium.*;
import org.openqa.selenium.edge.EdgeDriver;

public class RegistrationTest {
    public static void main(String[] args) {
        WebDriver driver = new EdgeDriver();

        driver.get("http://localhost:8084");

        driver.findElement(By.id("name")).sendKeys("Sreethan");
        driver.findElement(By.id("email")).sendKeys("test@gmail.com");
        driver.findElement(By.id("phone")).sendKeys("9876543210");
        driver.findElement(By.id("gender")).sendKeys("Male");
        driver.findElement(By.id("event")).sendKeys("Hackathon");

        driver.findElement(By.tagName("button")).click();

        String msg = driver.findElement(By.id("message")).getText();

        if (msg.equals("Registration Successful!"))
            System.out.println("Test Passed");
        else
            System.out.println("Test Failed");
    }
}
```

**Test Cases:**
| Test Case | Input / Action | Expected Result |
| :--- | :--- | :--- |
| **TC01** | Open application | Registration form displayed |
| **TC02** | Enter Name | Sreethan |
| **TC03** | Enter Email | test@gmail.com |
| **TC04** | Enter Phone | 9876543210 |
| **TC05** | Select Gender | Male |
| **TC06** | Select Event | Hackathon |
| **TC07** | Click Register | Registration Successful! |

**Execution Commands:**
```cmd
docker build -t registrationapp .
docker run -d -p 8084:80 registrationapp
```
