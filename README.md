# Prisoner's Dilemma - Correspondence Game

A URL-based Prisoner's Dilemma game built with the configurable correspondence games framework.

## Features

- ✅ **Config-driven**: Powered by YAML configuration
- ✅ **URL-based gameplay**: Share links to play asynchronously
- ✅ **Framework components**: Uses DynamicChoiceBoard and DynamicPayoffMatrix
- ✅ **5 rounds**: Classic iterated prisoner's dilemma
- ✅ **Classic payoffs**: Temptation (5), Reward (3), Punishment (1), Sucker's payoff (0)

## Quick Start

### Install & Run

```bash
# Install dependencies
npm install

# Start dev server
npm run dev
```

Open `http://localhost:5174/dilemma/`

### How to Play

1. **Player 1** starts the game and makes their choice (Stay Silent or Talk)
2. Copy the URL and send it to **Player 2**
3. **Player 2** opens the URL and makes their choice
4. Results are revealed and totals are updated
5. Repeat for 5 rounds
6. Winner is determined by highest total score

## Game Configuration

The game is defined in `games/configs/prisoners-dilemma.yaml`:

```yaml
metadata:
  id: prisoners-dilemma
  name: "Prisoner's Dilemma"
  version: "1.0.0"

choices:
  - id: silent
    label: "Stay Silent"
    description: "Cooperate with the other player by staying silent"
    icon: "🤐"

  - id: talk
    label: "Talk"
    description: "Betray the other player by talking to the authorities"
    icon: "🗣️"

# 4 payoff rules (2×2 combinations)
# Classic prisoner's dilemma payoffs:
# Both silent: (3, 3) - Reward for mutual cooperation
# Silent/Talk: (0, 5) - Sucker's payoff / Temptation to defect
# Talk/Silent: (5, 0) - Temptation to defect / Sucker's payoff
# Both talk: (1, 1) - Punishment for mutual defection
```

## Game Theory

The Prisoner's Dilemma is a classic game theory scenario that demonstrates why rational individuals might not cooperate, even when cooperation benefits both.

**Payoff Structure:**
- **Both Stay Silent (3, 3)**: Best collective outcome - moderate sentences
- **Both Talk (1, 1)**: Worst collective outcome - harsh sentences
- **One Talks, One Silent (5, 0)**: Betrayer goes free (5), silent one gets maximum sentence (0)

**The Dilemma**: Talking is always better individually (dominant strategy), but both talking is worse than both staying silent!

## Framework Components Used

### DynamicChoiceBoard
Renders choice buttons dynamically based on config:
- Adapts to any number of choices
- Shows icons and descriptions
- Applies theme colors

### DynamicPayoffMatrix
Displays payoff outcomes:
- Color-coded scores (green=positive, red=negative)
- Shows all possible combinations
- Outcome text for each scenario

### Game Engines
- **PayoffEngine**: Calculates scores from config rules
- **TurnEngine**: Manages round progression and alternation

## Project Structure

```
dilemma/
├── src/
│   ├── App.tsx                 # Main game logic
│   ├── main.tsx                # React entry point
│   ├── framework/              # Configurable framework
│   │   ├── core/
│   │   │   ├── config/         # YAML loader & validation
│   │   │   ├── schemas/        # Zod schemas
│   │   │   └── engine/         # Game logic engines
│   │   ├── components/         # Dynamic UI components
│   │   ├── hooks/              # React hooks
│   │   └── storage/            # Encryption utilities
│   └── shared/
│       └── utils/
│           └── constants.ts    # Game secret
│
├── games/configs/
│   └── prisoners-dilemma.yaml
│
├── package.json
├── vite.config.ts
└── tsconfig.json
```

## Available Scripts

```bash
npm run dev          # Start dev server (port 5174)
npm run build        # Build for production
npm run preview      # Preview production build
npm run type-check   # TypeScript validation
```

## Deployment

### GitHub Pages (Automated)

Simply run:
```bash
npm run deploy
```

This will:
1. Build the project
2. Push the `dist/` folder to the `gh-pages` branch
3. GitHub Pages will automatically serve from that branch

**First-time setup**: Make sure GitHub Pages is enabled in your repo settings and set to deploy from the `gh-pages` branch.

### Manual Deployment

1. Build the project:
   ```bash
   npm run build
   ```

2. Push the `dist/` directory to the `gh-pages` branch:
   ```bash
   git subtree push --prefix dist origin gh-pages
   ```

**Note**: The `vite.config.ts` is already configured with the correct base path: `/dilemma/`

## Customization

### Change Number of Rounds

Edit `games/configs/prisoners-dilemma.yaml`:

```yaml
progression:
  totalRounds: 10  # Change to any number
```

### Modify Payoffs

To adjust the payoff values (e.g., make cooperation more rewarding):

1. Edit the `payoffRules` section in the YAML config
2. Adjust the `outcome` values for each scenario
3. Framework handles the rest automatically!

### Theme Colors

```yaml
ui:
  primaryColor: "#3b82f6"      # Blue theme
  secondaryColor: "#8b5cf6"    # Purple accent
```

## Architecture

This game demonstrates the configurable framework's capabilities:

- **No hardcoded game logic** - everything from YAML
- **Dynamic UI generation** - adapts to config
- **Type-safe** - Zod validation at runtime
- **Reusable** - same components work for any game

## Strategy Tips

In iterated prisoner's dilemma (multiple rounds):
- **Tit-for-Tat**: Start silent, then copy opponent's last move
- **Always Defect**: Always talk (dominant strategy in single round)
- **Always Cooperate**: Always stay silent (risky but builds trust)
- **Forgiving Tit-for-Tat**: Occasionally forgive betrayals

## Related Games

- [Rock Paper Scissors](../rock-paper-scissors/) - 3 choices, 3 rounds
- Create your own game using this framework!

## License

MIT

---

Built with the [Correspondence Games Framework](https://github.com/your-org/correspondence-games-framework)
