# CKAX

CKA and CKAD Kubernetes Certifications are challenging: you do not only need to solve the tasks, you need to do it fast. For CKA, considering you want to save 12 minutes for reviewing your exam, that gives you around 4.5 minutes per task. In order to keep up with that pace, you need to train, and train hard.

_CKAX_ is a small but useful Python script that will present you with a series of CKA/CKAD tasks, randomly selected from a predefined list, and will measure how much time you take to solve each one. After finishing, you will be presented with a summary, so you can later focus on the topics that took you longer.

## Assumptions and requirements

- _CKAX_ has been tested on an Ubuntu 18.04 machine, but most likely any machine with `python3.6` should be able to run it without problems.
- All the tasks defined assume you have a cluster of 4 nodes. If you have a different amount of nodes in your cluster, please focus on what the task wants you to achieve to adapt it to your scenario.

## Usage

The script can be easily used out of the box with `python3`:

```
python3 ckax
```

This will trigger a series of randomly selected tasks. Once you are finished with a task, press `ENTER` to continue with the next one.

A summary with all tasks and the time spent on each of them will be shown once you have finished:

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│                                                                                  │
│                                   FINAL STATS                                    │
│                                                                                  │
├───────────┬───────────────────┬──────────────────────────────────────┬───────────┤
│  TASK 1   │STORAGE            │Create a pod called [...]             │1min 32sec │
├───────────┼───────────────────┼──────────────────────────────────────┼───────────┤
│  TASK 2   │CONFIGMAPS [...]   │Create a secret called [...]          │1min 49sec │
├───────────┼───────────────────┼──────────────────────────────────────┼───────────┤
│  TASK 3   │SERVICES AND [...] │Create two nginx deployments of [...] │ 1min 8sec │
├───────────┼───────────────────┼──────────────────────────────────────┼───────────┤
│  TASK 4   │STORAGE            │Create a 1 replica deployment of [...]│0min 57sec │
├───────────┼───────────────────┼──────────────────────────────────────┼───────────┤
│  TASK 5   │SERVICES AND [...] │Create a 3 replica deployment of [...]│1min 31sec │
└───────────┴───────────────────┴──────────────────────────────────────┴───────────┘
```

Two environment variables are supported for configuration: the `TASKS_AMOUNT` and `TASKS_FILE` variables. They default to `5` tasks and the local `tasks` file. You can override any of them when running the script.

```
TASKS_AMOUNT=10 TASKS_FILE=/home/ubuntu/mytasks python3 ckax
```

## Tasks file

Tasks are randomly chosen from a tasks file, which groups them into categories. Each category has a relative `weight` so the script will select them based on those weights. A weight of 0 will result in a category never getting selected, so you can edit the task file to disable any category. Inside a category, all questions can be randomly picked with equal probability.

The task file format follows the next structure:

```
[ CATEGORY1 ]

weight: 5

T1: Task 1 description.

T2: Task 2 description.

T3: ...

[ CATEGORY2 ]

weight: 8

T1: Task 1 description.

T2: ... 
```


