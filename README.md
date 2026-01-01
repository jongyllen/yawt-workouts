# yawt-workouts

Official workout program repository for [yawt (Yet Another Workout Tracker)](https://github.com/jongyllen/yawt).

This repository serves as the default registry for discoverable workout programs in the yawt app. Users can browse and import these programs directly from the app's "Discover" tab.

## Available Programs

| Program | Duration | Description |
|---------|----------|-------------|
| **28-Day Calisthenics Plan** | 4 weeks | Low-impact bodyweight training focused on foundation and form |
| **Hamstring Flexibility** | 2 weeks | Daily stretching routine to fix tight hamstrings |
| **50 Pushups Challenge** | 6 weeks | Progressive plan to achieve 50 consecutive pushups |
| **Yoga & Mobility** | 1 week | Morning and evening mobility flows |

## How It Works

The yawt app fetches the `registry.json` file from this repository to display available programs in the Discover tab. When a user selects a program, the app downloads the corresponding JSON file and imports it into their local library.

### Registry Format

The `registry.json` file contains a manifest of all available programs:

```json
{
    "programs": [
        {
            "id": "unique-program-id",
            "name": "Display Name",
            "description": "Short description of the program",
            "author": "Author Name",
            "path": "filename.json"
        }
    ]
}
```

## Program Schema

All workout programs follow the `workout.program.v1` schema. Here's the structure:

```json
{
    "id": "unique-id",
    "version": "workout.program.v1",
    "name": "Program Name",
    "description": "Program description",
    "weeks": [
        {
            "weekNumber": 1,
            "workouts": [
                { "dayNumber": 1, "workoutId": "workout-id" }
            ]
        }
    ],
    "workouts": [
        {
            "id": "workout-id",
            "name": "Workout Name",
            "blocks": [
                {
                    "id": "block-id",
                    "name": "Block Name",
                    "type": "warmup|main|cooldown|circuit|interval",
                    "rounds": 1,
                    "restBetweenRounds": 60,
                    "steps": [
                        {
                            "id": "step-id",
                            "type": "exercise_inline|rest|timer|hold",
                            "name": "Step Name",
                            "description": "Short tagline",
                            "instructions": "Detailed instructions",
                            "cues": ["Form cue 1", "Form cue 2"],
                            "durationSeconds": 30,
                            "reps": 10
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Step Types

| Type | Description |
|------|-------------|
| `exercise_inline` | An exercise with reps or duration |
| `rest` | A rest period |
| `timer` | A timed activity |
| `hold` | A static hold (like planks or stretches) |

### Block Types

| Type | Description |
|------|-------------|
| `warmup` | Warm-up exercises |
| `main` | Main workout |
| `cooldown` | Cool-down/stretching |
| `circuit` | Circuit training with multiple rounds |
| `interval` | Interval-based training |

## Contributing

Want to add your own workout program? 

1. Fork this repository
2. Create your program JSON file following the schema above
3. Add an entry to `registry.json`
4. Submit a pull request

### Guidelines

- Use descriptive, unique IDs for programs, workouts, blocks, and steps
- Include clear instructions and form cues for exercises
- Test your JSON for validity before submitting
- Keep descriptions concise but informative

## Using a Custom Registry

The yawt app can be configured to use a different registry repository. In the app's Settings, you can change:

- **Registry Repository**: The GitHub `username/repo` path (default: `jongyllen/yawt-workouts`)
- **Registry Branch**: The branch to fetch from (default: `main`)

This allows you to:
- Host your own private collection of workout programs
- Fork this repo and customize the available programs
- Point to your own GitHub repository with custom workouts

## License

This project is licensed under the [MIT License](LICENSE).
