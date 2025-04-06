# CrewAI Podcast episode planner & outline generator

This project uses CrewAI to simulate a podcast production team. AI agents collaborate to research a topic (and optional guest), structure an episode, generate talking points and questions, draft intro/outro snippets, and compile everything into a comprehensive episode plan.

This tool assists podcast creators by automating much of the pre-production planning process. It's designed to run in Google Colab.

## Features

*   **Topic & guest research:** Gathers background information, key facts, interesting angles, and guest expertise using web search.
*   **Episode structuring:** Proposes a logical flow with distinct segments and estimated timings.
*   **Content generation:** Creates relevant talking points and discussion prompts for each segment.
*   **Guest question drafting:** Generates insightful, open-ended questions tailored to the guest's background (if applicable).
*   **Script snippet writing:** Drafts host text for introductions and outros, including hooks and calls to action.
*   **Plan compilation:** Assembles all generated content into a single, organized episode plan document (Markdown).

## Requirements

*   Python 3.9+
*   Google Colab Environment (Recommended) or local Python setup.
*   **API Keys:**
    *   **OpenAI API Key:** For the language model (GPT-4 Turbo recommended for better quality). Requires a funded account or active credits from [platform.openai.com](https://platform.openai.com/).
    *   **Serper API Key:** For the `TopicResearcher` agent's web search via `SerperDevTool`. Get one from [serper.dev](https://serper.dev/) (free tier available).

## Setup (Google Colab)

1.  **Get the Notebook:** Clone the repository or download the `.ipynb` file.
2.  **Open in Colab:** Upload and open in Google Colab ([colab.research.google.com](https://colab.research.google.com/)).
3.  **Install libraries:** Run Cell 1 (`# @title 1. Install...`) to install necessary packages.
4.  **Configure API Keys in Colab Secrets:**
    *   Go to Colab Secrets (Key icon `<>` in the left sidebar).
    *   Enable "Notebook access".
    *   Add two secrets:
        *   Name: `OPENAI_API_KEY` | Value: Your OpenAI key (`sk-...`)
        *   Name: `SERPER_API_KEY` | Value: Your Serper key
    *   Make sure the **toggle switch** is **ON** for both secrets.
5.  **Run Cell 2:** Execute Cell 2 (`# @title 2. Import Modules...`). Check the output to verify both API keys were loaded successfully. Fix any errors before proceeding.

## How to Use

1.  **Define episode details (Cell 3):**
    *   Go to Cell 3 (`# @title 3. Define Podcast Episode Details`).
    *   **Modify the values** for `episode_topic`, `guest_name` (set to `None` or `""` if no guest), `guest_info_url` (if applicable), and `podcast_style`. Provide as much detail as relevant.
2.  **Select LLM (optional - Cell 4):**
    *   Ensure an appropriate model (GPT-4 Turbo recommended) is selected in Cell 4.
3.  **Run cells sequentially:** Execute Cells 4 through 8 in order.
    *   Cell 5 defines the agents.
    *   Cell 6 defines the tasks.
    *   **Cell 7** creates the `Crew` and runs `kickoff()`. This is the main step and will take time and API calls. Observe the verbose output to see the agents work.
    *   Cell 8 displays the final compiled episode plan.

## Workflow overview

1.  **Topic researcher (Task 1):** Researches the topic and guest (if any).
2.  **Episode structurer (Task 2):** Creates the segment outline and timings.
3.  **Content point generator (Task 3):** Develops talking points and guest questions for each segment.
4.  **Script element writer (Task 4):** Drafts intro and outro text.
5.  **Plan compiler (Task 5):** Assembles all parts into the final plan document.

## Customization

*   **Episode details:** Change inputs in Cell 3 for different episodes.
*   **Agent personalities:** Modify `role`, `goal`, `backstory` in Cell 5.
*   **Task specificity:** Adjust `description`, `expected_output` in Cell 6. For example, request more/fewer questions, different segment types, or a specific call to action.
*   **Structure/timing:** Change the requirements in the `EpisodeStructurer`'s goal/task description.
*   **Tools:** Add or replace research tools if you have access to different APIs or databases.

## Limitations

*   **API costs:** LLM usage costs money. Monitor your OpenAI spending.
*   **Research quality:** Depends on the search tool's effectiveness and the LLM's ability to synthesize information accurately. Web scraping/reading can be unreliable.
*   **Creativity:** While capable, the AI's creativity for hooks, questions, or unique angles might be limited compared to a human producer.
*   **Guest nuance:** Understanding a guest's true personality or subtle expertise from online info alone is difficult.
*   **This is an assistant:** The generated plan is a strong starting point but should be reviewed, edited, and adapted by the actual podcast host/producer.
