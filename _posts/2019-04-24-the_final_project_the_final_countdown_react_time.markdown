---
layout: post
title:      "The Final Project... The Final Countdown... REACT TIME! "
date:       2019-04-24 21:32:51 +0000
permalink:  the_final_project_the_final_countdown_react_time
---


My friend runs a fitness travel company called SurfYogaBeer. The company runs curated retreats all over the world with the focus of bringing people together through workouts and beer. I had the good fortune of going on a trip to Morocco with 33 other people, none of whom I had ever met until we first got on the plane. The experience was life changing for me as I made lifelong friends in the span of a week and  just reminded myself that even past college, it is possible to go on “spring break” eque trips where you can live carefree. 

Although a company with a strong mission, SYB could definitely benefit from an upgrade on their digital platforms. If you go to SYB’s site, you will notice right away that the site was built on a Squarespace platform. The UI experience is terrible and it is not too easy to book both trips and their local classes in NYC. Given that I have spent nearly eight months studying development, I decided to make an attempt to tackle a complicated part of the site that SYB does not have currently: a class booking platform. I feel that this would be the perfect way to challenge myself and practice everything we learned in the Flatiron curriculum. The project would require many different tables and associations that would make the project challenging in itself. Furthermore, I felt building out the front end of the platform in React would push me to go beyond the concepts we learned in the curriculum and force myself to study external resources. The end goal here is to build a site that is similar to that of rumble.com or tonehouse.com. 

Overall, I really enjoyed working on this project. I will note it’s not finished and that I plan on working on this project over the next few months as it is rather complex and will take time to build properly. There were some ups and downs but for the main part this project was very fun to build out. 

Rails 

DB Migration 
I created eleven tables that I migrated into a SQL database: workouts, workout_payments, users, schedules, oauth_applications, oauth_accesstokens, oauth_accessgrants, jwt_blacklist, instructors, clients, and bookings. The new concept here that differs from my other projects is that I tried to implement doorkeepr and devise. These two libraries are well known for building out thorough authentications systems. The goal here was to provide a user a token via a cookie once he/she logged in or signed up. This is different from my past projects where I built out the logic manually using the application and sessions controller.
 Although both devise and door keeper are two well known gems that both have over a million downloads on the ruby gem site, I did find implementing these libraries was difficult. The biggest challenge was that a lot of the documentation for these libraries were for developers who were building out the front-end using Rails as well. In this project, I not only built out the backend as an API, I also built it out with the intention of keeping it in an entirely separate from the front-end interface. After reading several documentations and blogs on how to build out a backend API in Rails while implementing the front-end using React/Redux, I finally was able to create the scaffolding for the project that I later built on in the last two weeks. Now, if a user were to fire up the front-end on their local host while simultaneously running the backend on a separate port, the first thing he/she would notice is once signed up or logged in, the browser is automatically given an authentication key via a cookie which is constantly checked on when the user makes a request to the API. MAGICCCCCC!!!	

Models & Serializers
The project has nine models and seven serializers. The models are pretty straight forward. The one section to highlight is the way the user, client and instructor models are organized and how the workout, schedule and booking models are associated. For the first set of relationships, I thought of the user as an account. There are three types of users: admin, instructor, and client. I set the system up so that a person accessing the front-end is automatically assumed to be a client. In order to be an admin or an instructor, that would have to be made manually on the backend. I felt this would be a lot easier and plan to build out an interface for both admins and instructors so they can manage both their accounts but also have control over what is shown on the client-facing side of the app. The second set of associations is rather interesting as it really made me think about how these other fitness booking sites are created. After conducting my own research, I decided to build out 5 different tables to tackle the issue, but the core three are the workouts, schedules and bookings table. The parent of the group is the workout table. The workout model has many schedules. A schedule belongs to an instructor and has many bookings. For visualization purposes, please refer to the image to the left. Here, you would be looking at multiple schedules that belong to a trainer and a workout. Each of these schedules has a certain number of bookings (slots available) for clients to register for the class. After a few trail and errors, I was able to get this to work. The associations come full circle as a Client has many bookings allowing the front-end to show a user how many classes he/she is signed up for when looking at their personal profile page. 

Next, you will see that I also created seven serializers. The serializers are pretty straightforward, as they correspond to the models mentioned above. I pulled in almost all the information and made sure to add the associations so I could limit the amount of API calls I needed to make when using the React front-end. 
	
III. Controllers 

I built out 9 controllers. The most exciting aspect of these controllers is how they are all structured. If one were to look at the API via text editor such as Sublime, one would notice the folders are in a controller folder as usual, but after then nested in a api/v1 folder and have a different structure when declaring the class on the first line of each controller compared to a standard rails controller: class Api::V1::InstructorsController < ApplicationController
Here, the way the folders are organized allows a couple things. One, when a user makes a call for the API, the url actually has api in it, which in my opinion makes this more legit. Second, as this project gets more advanced and as I continue to implement various access parameters etc, I can start implementing various versions, which would just mean I could copy V1 folder and start implementing new versions with various tweaks to the controller (version control). 

IV. Overall Backend Rails 

Overall, I found building out this rails backend to be the most challenging project I have done so far in my early coding career, which I find ironic considering the main part of the project was supposed to be React/Redux. That being said, I learned a lot during the implementation of this part of the project and found it to be a lot of fun. Again, the biggest challenge here was just thinking about this solely as an API. I spent a LOT of time figuring out how to generate authentication tokens and passing this information via a session cookie. I am really glad I went down this tunnel, as it helped me learn a lot of about cyber security and the different ways sites implement login/signup authentication. 


React 

Packages 
I have 14 dependencies in this project.  
```
   "axios": "^0.18.0",
   "lodash.map": "^4.6.0",
   "luxon": "^1.12.1",
   "prop-types": "^15.7.2",
   "react": "^16.8.6",
   "react-dom": "^16.8.6",
   "react-portal": "^4.2.0",
   "react-redux": "^7.0.1",
   "react-router": "^5.0.0",
   "react-router-dom": "^5.0.0",
   "react-scripts": "2.1.8",
   "redux": "^4.0.1",
   "save": "^2.3.3",
   "styled-components": "^4.2.0"
```

The more interesting ones to note here are axios, lodash, luxon, and save. Based on a lot of what I have read, axios is the industry standard for fetching data so I decided to use that for all GET and POST requests made to my backend API. I found the documentation to be easily digestible which allowed me to seamlessly integrate the library into the project. Second, I imported lodash, which actually allowed me to use a method that is similar to the pluck method one could use in Ruby. Lastly, I used Luxon to help format all the datetimes I used in my calendar component. 

II. Components 

I have a lot of components in this project, so for the sake of my readers, I will just highlight some of my favorite parts of the React app. The best part of the app by far is the calendar section where a user can book an app. In the actual workout component (think of this as a calendar), I am doing several complex things that all come together and render this type of calendar. First, I am making a call to the workouts portion of my API which gives me access to not only all workout data, but everything that falls underneath it… which if you all remember includes schedules, booking and instructor data. I then am able to use both lodash and luxon to map over all the data and render it out in a grid that I created using javascript. Next, with some grid-css, I am able to create a calendar that looks something like this! Again, similar to the challenge I faced when creating these associations in the backend, was just organizing the React app to actually render and function the way it’s supposed to in that a user can view a a workout and all the bookings available for each day, and then actually book a class which will automatically update in the users account and even show up when it’s time to pay for the class. I spent a lot of time on this portion of the project and am still going to continue to build on it as I continue working on the project. 

III. Redux <> Overall React 

I found Redux extremely cool but kind of confusing at the same time. But what is helpful is to kind of think of it outside of the code and just put it into layman terms, so here we go...  

You have a central store that houses the reducers and will trigger updates to any of the components that subscribe to these updates. Which, actually lets start there... components subscribe to these updates that are available via the store. The store is created in the main part of the app, which in my projects case is actually in App.js. The store is available through Provider, which is wrapped around all the components that are rendered on the DOM. So moving on to the components, these all have the ability to actually dispatch actions, which then will reach our handy-dandy reducer. The reducer here will receive the action and update the state, which then will update the central store. The central store will then update any of the states of components that subscribe to these updates. AND BOOOOOM that is the full circle. I definitely generalized this process by a lot, but this is how I understand the process. What I really found interesting was the concept of breaking all these pieces down. If you refer to my project, you will notice I actually have all my actions completely separate from the reducer. I import these actions, well the ones I use in each component, and use these as part of the dispatch. These actions will hit my master action pages, which will then communicate with the reducer to perform what it needs to do to the state before sending that updated state to the components. This process took some time to get the hang of, but I am really proud of what I have done so far. Here's a snap shot of one of my action pages and one of my reducers for the clients. It took quite some time to organize, but I think the outcome works quite well: 

# Action -- Client Builder
```
import * as actionTypes from './actionTypes';
import axios from "axios";
import { axiosInstance } from "../../services";
import { setLoading } from './spinnerBuilder'


export const removedClass = ( bookingId ) => {
    return {
        type: actionTypes.REMOVE_CLASS,
        bookingId
    };
};

export const setClient = ( clientData ) => {
    return {
        type: actionTypes.SET_CLIENT,
        clientData
    };
};

export const fetchClientFailed = () => {
    return {
        type: actionTypes.FETCH_CLIENT_FAILED
    };
};

export const initClient = () => {
    return dispatch => {
      const id = localStorage.getItem("clientID"); 
      dispatch(setLoading(true));
      axiosInstance
        .get(`/api/clients/${id}`) 
            .then( response => {
                dispatch(setLoading(false));
               dispatch(setClient(response.data));
            } )
            .catch( error => {
                dispatch(setLoading(false));
                dispatch(fetchClientFailed());
            } );
    };
};

export const removeClass = (bookingId) => {
    console.log('C')
    return dispatch => {
        const id = localStorage.getItem("clientID"); 
        dispatch(setLoading(true));
        axiosInstance
          .delete(`/api/bookings/${bookingId}`) 
              .then( response => {
                  console.log('D')
                dispatch(setLoading(false));
                 dispatch(removedClass(bookingId));
              } )
              .catch( error => {
                dispatch(setLoading(false));
                  dispatch(fetchClientFailed());
              } );
      };
      console.log('E')
}
```

# Reducer -- Client Reducer 
```
import * as actionTypes from '../actions/actionTypes';
import { updateObject } from '../utility';

const initialState = {
  user: {}, 
  clientId:"",
  clientData: {
    bookings: []
  }
};
 
const setClient = (state, action) => {
  return updateObject( state, {
      clientData: action.clientData
  } );
};

const fetchClientFailed = (state, action) => {
  return updateObject( state, { error: true } );
};
const removedClass = (state, action) => {
  return updateObject(state, {clientData: updateObject(state.clientData, {bookings: state.clientData.bookings.filter((booking) => booking.id !== action.bookingId)})})
}


const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.SET_LOGIN_SUCCESSFUL:
      return {
        ...state,
        ...action.payload
      }
    case actionTypes.REMOVE_ACCESS_TOKEN: 
        return {
          ...state,
          user: {},
          accessToken: ""
      }
    case actionTypes.SET_CLIENT: return setClient(state, action);    
    case actionTypes.FETCH_CLIENT_FAILED: return fetchClientFailed(state, action);
    case actionTypes.REMOVE_CLASS:
    return removedClass(state, action)
    }
    
    return state;
  }; 

  export default reducer;
```


III. Overall 
	The judgement is still out on React and definitely still out for Redux. I understand the appeal. The fact that React has both State and Props makes the framework extremely interesting. I'm sure as I continue learning React, I will love the way in which this is all organized and will only want to use React to build out apps! I also enjoyed learning about Redux. The fact that State, a single source of truth, to me, makes it seem like an API. Redux is fascinating and I enjoyed implementing it in my application. I found the asyc actions a little hard to grasp at times, but there are a lot of resources out there that really get into these topics, such as Wes Bos. I am definitely going to continue working on this project, and hopefully continue to build on these foundations I have developed so far! 

