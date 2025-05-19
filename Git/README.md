
# GitStartedWithUs

Welcome to GitStartedWithUs, a collaborative platform for creative individuals to color pixels, leave their mark, and express themselves through art! Here you have the opportunity to contribute to a collective canvas by coloring individual pixels and sharing your unique identity with the world.

## Resources:

1. An Intro to Git and GitHub for Beginners 
    
    🔗 https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners

2. Git Commands Cheat Sheet

    📄 A concise README-style Git cheat sheet repository

    🔗 https://github.com/joshnh/Git-Commands
    
    📝 Lists common Git commands with brief explanations. Great for quick reference.

 

3. GitFlight-Rules
    📄 A repository of "what to do when" scenarios for Git
    
    🔗 https://github.com/k88hudson/git-flight-rules
    
    📝 Use this like an emergency manual for tricky Git situations. The README and structure are excellent for real-world use.

4. Git-Tips
    
    📄 Useful Git tips and tricks in a README
    
    🔗 https://github.com/git-tips/tips
    
    📝 Crowdsourced tips that range from beginner to advanced.



## Getting started

To get started with coloring pixels and leaving your mark on the canvas, follow these simple steps:

- **Explore the Canvas**: Visit the Pixels website and explore the interactive canvas filled with blank pixels waiting to be colored. Each pixel represents a tiny square on the canvas.
- **Choose Your Color**: Select your preferred color from the color palette available. We offer a diverse range of colors to choose from, allowing you to create eye-catching and imaginative designs.
- **Color a Pixel**: Click on an individual pixel to color it with your chosen color. Watch as your pixel contributes to the evolving masterpiece on the canvas.
- **Submit Your Contribution**: Once you've colored your pixel, you can submit your contribution.

## How to Contribute

Contributing to the canvas is easy and enjoyable:

- **Fork** the repository
- **Clone** it and create a `new branch`
- **Choose Your Pixel**: Select a pixel you'd like to color.
- **Pick Your Color**: Go to the style.css, choose your preferred color from the palette and add it to your grid.
    - Copy the part where colours are specified at the end.
    - Add your colour and desired cell number.
    - Make sure you are not changing the existing code. Just paste your code at the end of style.css file
    - Save your changes
    - Check if your changes are being applied or not.
- **Commit changes**: Run the following commands
  ```bash
  git add style.css
  git commit -m "<cell_number>_<name>"
  ```
  If everything works correctly you are ready to push.
  ```bash
  git push -u origin <branch_name>
  ```
  
- **Creating PR**: 
    - Go to contribute on your forked repo
    - There you will find option to open a Pull Request (PR)
    - Click it and wait for review