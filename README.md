# Music Informatics: Final Project, Spring 2024

- Vasileios Katsaitis  (1115202000073)
- Dimokritos Kolitsos  (1115201900085)
- Konstantinos Chousos (1115202000215) 

## Relevant files

The whole implementation of our recommendation system exists in [this notebook](./recommendation_system.ipynb).

Our report is in the `docs/` directory.

## Setup

1. Create the virtual environment (for guaranteed compatibility, use python version 3.10).

    ```sh
    $ python3.10 -m venv venv
    ```

2. Enable it.

    ```sh
    $ source venv/bin/activate # if using a bash-like shell
    ```

3. Install the required libraries

    ```sh
    (venv) $ pip install -r requirements.txt
    ```

## How to run

> [!TIP]
> 
> If your computer runs out of memory on the demucs voice separation cell, you can
> restart your IPython kernel and simply load the previous dataframes from the generated
> pickle files, to save memory from some previous cells.
