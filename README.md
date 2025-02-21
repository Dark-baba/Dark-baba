<h1>Hi 👋, I'm Dark-baba</h1>
<p>Enjoy programme  and fu🖕k your Opinion </p>
<h2>🚀 Languages and Tools I Use</h2>
<p><a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="linux" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/photoshop/photoshop-line.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/photoshop/photoshop-line.svg" alt="photoshop" width="42" height="42" /></a>
<a target="_blank" href="https://www.vectorlogo.zone/logos/adobe_illustrator/adobe_illustrator-icon.svg" style="display: inline-block;"><img src="https://www.vectorlogo.zone/logos/adobe_illustrator/adobe_illustrator-icon.svg" alt="illustrator" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="42" height="42" /></a></p>
<p><img align="center" src="https://github-readme-stats.vercel.app/api?username=Dark-baba&show_icons=true&locale=en" alt="Dark-baba" /></p>
<p><img align="center" src="https://github-readme-streak-stats.herokuapp.com/?user=Dark-baba&" alt="Dark-baba" /></p>
<p><img src="https://github-readme-stats.vercel.app/api/top-langs?username=Dark-baba&show_icons=true&locale=en&layout=compact" alt="Dark-baba" /></p>
<p><a href="https://github.com/ryo-ma/github-profile-trophy"><img src="https://github-profile-trophy.vercel.app/?username=Dark-baba" alt="Dark-baba" /></a></p>


name: GitHub Snake Game

on:
  # Schedule the workflow to run daily at midnight UTC
  schedule:
    - cron: "0 0 * * *"
  # Allow manual triggering of the workflow
  workflow_dispatch:
  # Trigger the workflow on pushes to the main branch
  push:
    branches:
      - main
jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      # Step 1: Checkout the repository
      - name: Checkout Repository
        uses: actions/checkout@v3
      # Step 2: Generate the snake animations
      - name: Generate GitHub Contributions Snake Animations
        uses: Platane/snk@v3
        with:
          # GitHub username to generate the animation for
          github_user_name: ${{ github.repository_owner }}
          # Define the output files and their configurations
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      # Step 3: Deploy the generated files to the 'output' branch
      - name: Deploy to Output Branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          # Optionally, you can set a custom commit message
          commit_message: "Update snake animation [skip ci]"
