# How to run promptfoo in Docker container?

1. Clone promptfoo repository to some folder, for example "../promptfoo".
    ```sh
        git clone https://github.com/promptfoo/promptfoo 
    ```

    I have these 2 folders:
    ```sh
        ls -a .. | grep promptfoo
        promptfoo
        promptfoo-docker
    ```

2. Check and update env variables in file `promptfoo.env`. Sample file with structure: `promptfoo.env.sample`.
    ```yaml
        # Disable telemetry
        PROMPTFOO_DISABLE_TELEMETRY=1

        OPENAI_API_KEY=your_api_key

        OLLAMA_BASE_URL="http://host.docker.internal:11434"
    ```
3. Create, build and run promptfoo container with docker-compose.yml:
    ```sh
        docker compose up -d --build
    ``` 

## Working with Web UI

Open URL: http://localhost:3333

## Working with CLI

1. List running containers:
    ```sh
        docker container ls | grep promptfoo
        f95d9a8d9aa1   promptfoo-docker-promptfoo   "docker-entrypoint.s…"   3 days ago   Up 3 minutes (healthy)   0.0.0.0:3333->3000/tcp   promptfoo
    ```
2. Connect to container shell
    ```
        docker exec -it f95d9a8d9aa1 bin/sh
    ```
3. Jump to `evals` folder and setup new project with:
    ```sh
        cd evals
        promptfoo init project_folder_name
    ```
4. Go inside `project_folder_name` and run:
    ```sh
        cd project_folder_name
        promptfoo eval
    ```

More info you about promptfoo CLI you can find in docs: https://www.promptfoo.dev/docs/usage/command-line/


## Tips & Tricks commands

1. If you use local Ollama, then limiting concurrent jobs by `-j` parameter could be helpfull, for example: 
    ```sh
        promptfoo eval -j 2
    ```
2. Export eval to HTML:
    ```sh
        promptfoo eval -j 2 -o eval_output.html
    ```

3. Export eval to JSON
    ```sh
        promptfoo export eval-2024-09-23T08:09:37 > eval-2024-09-23-08-09-37.json
    ```
