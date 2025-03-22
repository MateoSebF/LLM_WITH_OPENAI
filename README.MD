# LLM wit OpenAI

In this project, we are integrating the OpenAI API and providing it with specific context to enable the language model (LLM) to make predictions based on the particular information you provide.

## Getting Started

To get started with this project, we will be using Python 3 and the following dependencies:

```bash
pip install openai

pip install -qU langchain-pinecone pinecone-notebooks

pip install -qU langchain-openai

pip install --quiet --upgrade langchain-text-splitters langchain-community langgraph

pip install -qU langchain-core
```
Additionally, you can open and run the provided Google Colab notebook for easy setup and execution:

Additionally, you can open and run the provided Google Colab notebook for easy setup and execution:

[Open the Colab notebook](https://colab.research.google.com/drive/1U9VIQlsKt-EzSap12xb6iaE203YJHJp_)

---

### Prerequisites

Before you begin, make sure you have the following prerequisites:

- Python 3.x installed on your machine.
- A valid [OpenAI API key](https://beta.openai.com/signup/) to interact with the models.
- A [Pinecone account](https://www.pinecone.io/start/). You'll need to create an index in Pinecone for storing data.
- A [LangSmith APi key](https://docs.smith.langchain.com/).

### Installing
Clone this repository to your local machine:
```
git clone <repository_url>
cd <repository_folder>
```

Install the required dependencies


### Architecture
To understand the architecture followed in this article, we are going to use a diagram like this:

![Class Diagram](images/Class_Diagram.png)

In this architecture, we extend the structure of Lab5_AREP with the login system by defining the interaction between key components to ensure secure authentication. The design consists of four main components:

User: This is the model class where we define user-related attributes, such as id, email, and password. It is annotated with @Entity, indicating that it represents a table in the database.

UserRepository: This interface extends JpaRepository and allows interaction with the database, enabling operations such as saving, deleting, and retrieving user data. It is annotated with @Repository, making it injectable into the UserService.

UserService: This class contains the business logic for user authentication and management. It handles operations like user registration, password encoding, and authentication validation. It interacts with UserRepository to fetch or update user data securely.

UserController: This class serves as the entry point for authentication-related operations. It is annotated with @RestController and exposes endpoints such as /auth/register and /auth/login. The controller processes authentication requests, validates user credentials, and returns appropriate responses, such as JWT tokens for secure session management.

This architecture ensures a clear separation of concerns, making the system maintainable and scalable. Security measures, such as password hashing using BCryptPasswordEncoder.

# Deployment
To deploy this project, we use a Docker-based solution on AWS, ensuring a secure and scalable setup.

## AWS Deployment
To deploy the application on AWS, we performed the following steps:

1. Created two EC2 instances—one for the backend and one for the frontend.
2. Configured security rules to allow inbound traffic on the required ports:
    - 80 and 443 for HTTPS access.
    - 3306 for MySQL (restricted access).
3. Assigned an Elastic IP to each instance to ensure a static address.
4. Configured a custom domain using Duck DNS, associating it with the Elastic IPs.
5. Installed Let's Encrypt and Certbot on both instances to generate SSL certificates, enabling secure HTTPS connections for both the frontend and backend.

## Backend Deployment
1. Installed Git and Docker on the EC2 instance.

2. Cloned the repository and navigated to the backend folder.

3. Ran the following command to build and start the backend and database containers:

```
docker-compose up --build -d
```

4. This command builds the backend image and deploys both the backend and MySQL containers.
5. The application now runs securely with HTTPS, as seen in the deployment demo.

## Frontend Deployment
1. Installed Git and Docker on the frontend EC2 instance.

2. Cloned the repository and navigated to the frontend folder.

3. Built the frontend Docker image using:

```
docker build -t frontend-app .
```
4. Ran the frontend container using:

```
docker run -d -p 80:80 -p 443:443 --name frontend-container frontend-app
```
5. The frontend is now accessible via the configured Duck DNS domain over HTTPS.

### Link to Deployment Demo Demostration 

[Watch the deployment in action](https://pruebacorreoescuelaingeduco.sharepoint.com/sites/Reco842/Shared%20Documents/General/Recordings/Reuni%C3%B3n%20en%20_General_-20250314_011913-Grabaci%C3%B3n%20de%20la%20reuni%C3%B3n.mp4?web=1&referrer=Teams.TEAMS-WEB&referrerScenario=MeetingChicletGetLink.view)  


## Built With

* [Java](https://www.oracle.com/co/java/technologies/downloads/) - The programming language used
* [Maven](https://maven.apache.org/) - Dependency Management
* [JUnit](https://junit.org/junit5/) - Testing Framework for unit tests

## Versioning

We use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) for versioning.  

## Authors

**Mateo Forero** - *Initial work* - [MateoSebF](https://github.com/MateoSebF)

## Acknowledgments

* Inspiration from various resources and tutorials