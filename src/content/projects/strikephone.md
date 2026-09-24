---
title: 'Strike Phone'
description: 'CUHackit 2025'
pubDate: 'Jul 08 2022'
heroImage: '../../assets/strikephone.png'
featured: true
---
### Context
This project was built for Clemson University's annual hackathon, CUHackit 2025. <br>
Link to the DevPost: https://devpost.com/software/strikephone <br>
Winner of the THE IRON MAN AWARD: MOST INNOVATIVE

### Inspiration
Our group plays a lot of blitzball, which is a game that is similar to baseball. The advantage that blitzball has over baseball is that the ball that is used is much lighter, enabling it to spin and curve much more, especially when pitching. The issue that comes with this is that it can be hard to tell what pitches were balls and what pitches are strikes.

### What it does
StrikePhone is an app that will take care of the ball/strike calling issue for you! It works by the user setting their phone up behind home plate. The user sets the camera up, takes a quick calibration image, and then records each pitch. After each pitch is recorded, the app returns whether it is a ball or a strike and displays it to the user. StrikePhone makes blitzball easier to play and avoids arguments over whether a pitch is a ball or a strike!

### How we built it
We separated this project into multiple stages and delegated each part to a different member of the group. We had individual group members working on overall UI and app development, ball tracking, and AI body tracking for strike zone generation.

For Front End: We used Expo Go with React Native to be able to develop code and test it locally on our phones as we developed the app. Expo Go allowed us for extremely quick front end development as well as recording videos and taking pictures that we were able to send to the s3 buckets.

For AI Body Tracking: We used Amazon AWS Rekognition, s3 buckets to store images, and Amazon AWS Lambda function to determine where the person is and generate a strike zone determined by that. These strike zone coordinates are returned by the function for the app to use to determine whether the ball is in the correct portion of the screen or not.

For ball tracking: Ball tracking was implemented using opencv and Hough Circle tracking. We are looking for baseballs/blitzballs, which are circular. We input an expected radius into our strikeDetection code, and that analyzes each frame. When the circle/ball matches the expected radius, we check to see if the position of the ball is inside the strike zone coordinates. If it is, then it is counted as a strike, otherwise it is a ball.

We weren't able to get all the modules working with one another under the same app, but the vision is as follows: After front end of the app would send a calibration image and pitching videos to the s3 bucket, the ball tracking system would constantly grab the latest calibration image, pitching video, and coordinates for the strike zone via the AI Body Tracking. It would then post a json file to the same s3 bucket containing json data for whether or not there was a strike. The json file would have the same name as the video posted in which the app would recognize that, pull the json file, and display whether or not there was a strike or ball.

### Challenges we ran into
Most of the AI models we wanted to use to track the ball and batter were not compatible with Expo Go and IOS, so we needed to compromise by using a Lambda function with AWS to process with python on the backend. The members of our group had never interacted with AWS as well, so a large portion of our project was researching and learning about Lambda, APIs, permissions and roles, and other AWS policies. We also struggled with integrating all of the functionalities together once they were working. We delegated the tasks to where each person was working on a different functionality, and when these were completed, we ran out of time before we could smoothly integrate it all together into one program. Because of this, we have individual programs that can track a ball, generate a strike zone, and a base app that can take a picture to calibrate and a video to ultimately send to the ball tracking software.

### Accomplishments that we're proud of
We’re very proud of being able to interact with the AWS server via the s3 buckets. We had a lot of trouble uploading the data and we’ve never worked with a server this intensely before. Additionally, we’re very proud of our team work and work delegation.

### What we learned
This project was an intense learning stretch for our entire group, since we had never worked with AWS or AI models before. While we weren’t able to make a polished final product, we learned a lot about needing to communicate and share code frequently throughout the development process to ensure that our functionalities can easily communicate with each other. Additionally, we learned a lot about app development, Expo Go, JavaScript and TypeScript.

### What's next for Strikephone
The first thing we plan to do next is making all of the systems work together in one fully functioning user interface. We have several features that we plan to implement in the future, including a live replay to show the players where the ball or pitch was after it was thrown. We fully intend to continue working on the project in the future!