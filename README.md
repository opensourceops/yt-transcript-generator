# YouTube Transcription Docker Project

This project allows you to download, process, and transcribe YouTube videos using AssemblyAI. The entire process is containerized using Docker, making it easy to set up and run on any machine.

## Prerequisites

Before you can run this project, ensure you have the following:

- **Docker**: Installed on your machine. You can download Docker from [here](https://docs.docker.com/get-docker/).
- **AssemblyAI Account**: Sign up for a free account at [AssemblyAI](https://www.assemblyai.com/) to obtain an API key.

## Setting Up AssemblyAI

1. **Sign Up for AssemblyAI**:
   - Go to [AssemblyAI's website](https://www.assemblyai.com/) and sign up for a free account.
   - After signing up, navigate to your dashboard where you'll find your API key. Copy this key, as you'll need it in the next step.

2. **Create a `.env` File**:
   - In your project directory (the directory where you will run the Docker container), create a `.env` file. This file will store your AssemblyAI API key.
   - Add the following line to the `.env` file:
     ```bash
     ASSEMBLYAI_API_KEY="<YOUR_API_KEY>"
     ```
   - Replace `<YOUR_API_KEY>` with the API key you copied from the AssemblyAI dashboard.

   Example `.env` file:
   ```bash
   ASSEMBLYAI_API_KEY="1234567890abcdef1234567890abcdef"
   ```

3. **Save the `.env` File**:
   - Make sure the `.env` file is saved in the directory where you will be running the Docker commands.

## Pulling and Running the Docker Image

Follow these steps to pull the Docker image and run the transcription process:

1. **Pull the Docker Image**:
   - Pull the pre-built Docker image from Docker Hub using the following command:
     ```bash
     docker pull agentmaddy/yt-transcription
     ```

2. **Run the Docker Container**:
   - Use the following command to run the Docker container. This command mounts your current directory to the `/app` directory inside the container and runs the transcription script.
   - Replace `FILE_NAME` with your desired output file name and the YouTube URL with the URL of the video you want to transcribe.
     ```bash
     docker run -v $(pwd):/app agentmaddy/yt-transcription python app.py -o FILE_NAME --urls https://www.youtube.com/watch?v=KUECJHlV1LE
     ```

   - **Explanation**:
     - `-v $(pwd):/app`: Mounts the current directory on your local machine to the `/app` directory inside the Docker container. This allows the container to save output files directly to your local directory.
     - `agentmaddy/yt-transcription`: The Docker image you pulled from Docker Hub.
     - `python app.py -o FILE_NAME --urls https://www.youtube.com/watch?v=KUECJHlV1LE`: The command run inside the container, where `app.py` processes the YouTube video, extracts the audio, and generates a transcription.

3. **Accessing the Output**:
   - The output files, including the `.mp3` audio file and the transcription `.txt` file, will be saved in the directory where you ran the Docker command.
   - For example, if you run the command from `/home/user/projects`, the output files will be saved in `/home/user/projects`.

## Example Usage

To transcribe a YouTube video with the title "How to Dockerize Your Python Applications", you would run the following:

```bash
docker run -v $(pwd):/app agentmaddy/yt-transcription python app.py -o docker_tutorial --urls https://www.youtube.com/watch?v=KUECJHlV1LE
```

- This command will download the video, extract the audio, and save the transcription as `docker_tutorial_transcript.txt` in your current directory.

## Troubleshooting

- **Docker Not Found**: Make sure Docker is installed and running on your machine.
- **Invalid API Key**: Ensure your `.env` file is correctly set up with a valid AssemblyAI API key.
- **Permission Issues**: If you encounter permission issues when running the Docker container, try running the command with `sudo`.


### Summary of the Steps:

1. **Set Up AssemblyAI**: Sign up, obtain an API key, and create a `.env` file with the API key.
2. **Pull Docker Image**: Use `docker pull agentmaddy/yt-transcription` to get the image.
3. **Run the Docker Container**: Execute the Docker command with your desired output file name and YouTube URL.

This documentation provides a comprehensive guide on how to set up and use your Dockerized YouTube transcription project. You can add this content to your `README.md` file in your GitHub repository to guide users through the process. Let me know if you need further assistance!
