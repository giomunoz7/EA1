# EA1
# New Coug Advisor – Hackathon Project 

## Overview
New Coug Advisor is a project created during a hackathon to help new Washington State University students find important campus resources and start planning their academic path. When students first arrive at WSU, it can be difficult to figure out things like majors, campus opportunities, and where to find helpful information. The goal of this project was to create a simple platform where students could sign up, explore events that relate to their major and begin generating an academic plan.

## My Role
For this project, I worked mainly on the frontend of the application. I built the landing page where students can either sign up for the platform or log in to retrieve their academic plan.

The landing page includes a form where users can enter their username, first name, last name, and major. I also added a toggle that lets users switch between **Sign Up** and **Log In** without leaving the page. My focus was making the interface simple, clean, and easy for new students to understand.

## Code sample
const [mode, setMode] = useState('Sign Up')
const [isLoading, setIsLoading] = useState(false);

const onFinish = async (values: FormValues) => {
  setIsLoading(true);

  try {
    if (mode === "Log In") {
      const response = await axios.get(
        "http://127.0.0.1:5000/fetch-student",
        { params: { username: values.username } }
      );

      const data = response.data;

      if (data.result) {
        setLogin(true);
        setUser({
          username: data.user.username,
          firstName: data.user.first_name,
          lastName: data.user.last_name,
          major: data.user.major
        });
      } else {
        alert(data.message || "User not found.");
      }
    } else {
      const response = await axios.post(
        "http://127.0.0.1:5000/create-student",
        {
          username: values.username,
          first_name: values.firstName,
          last_name: values.lastName,
          major: values.major
        }
      );

      const data = response.data;

      if (data.result) {
        setLogin(true);
        setUser(values);
        alert("Generating your academic plan...");
      } else {
        alert(data.message || "Something went wrong.");
      }
    }
  } catch (error) {
    alert("Server error. Make sure Flask is running.");
  } finally {
    setIsLoading(false);
  }
};

## What the Code Does
The code I wrote controls the main landing page of the site. Some of the key things it does include:

- Creating a **Sign Up / Log In toggle** so users can switch modes easily  
- Displaying different form fields depending on the selected mode  
- Allowing users to choose their major from a searchable list of **WSU majors**  
- Managing form input using React state  
- Sending requests to a backend server using **Axios**  
- Logging in or creating a student profile depending on the action  

The page is styled using WSU-themed colors and a centered card layout so it looks organized and professional.

## Technologies Used
This project used several modern web development tools:

- **React** – for building the user interface  
- **Vite** – for development and fast builds  
- **TypeScript** – for better structure and type safety  
- **Ant Design** – for UI components like forms, cards, buttons, and dropdowns  
- **Axios** – for connecting the frontend to the backend API  
- **GitHub** – for version control and project collaboration  

## Technical Decisions
One decision I made was to keep the Sign Up and Log In features inside the same component. Instead of creating separate pages, I used React state to switch between the two modes. This helped keep the interface simple and easier to manage.

I also used Ant Design components because they provide clean UI elements that make forms and layouts easier to build while still looking professional.

## Reflection
Working on this project has given me an opportunity to build a real interface with React. In terms of the landing page, I wanted to create something simple enough for new students to use, but also not too simple as to make them feel overwhelmed or confused. One major challenge I had was to organize the form so that it could be used for both signing up and logging in, while still keeping the page from being too cluttered. The use of React state allowed me to accomplish this goal, by creating an interface that changes based on what the user is doing. I believe my portion of this project has been valuable as it will likely be the first interaction the users have with our application. If I were to continue working on this project I would look to improve the current loading feedback, improve error handling and add additional personalized features for students.

## Proof of Participation
- Group members were Kevin and Lyke
- A screenshot of my discord name joining the CrimsonCode discord. Name is yunggio.

