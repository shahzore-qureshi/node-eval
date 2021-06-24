# NODE EVAL

Follow the instructions below and complete the work to the best of your ability.

## Set up

- Clone this repository: [Node Eval](https://github.com/shahzore-qureshi/node-eval)
- Run `npm install`
- Add [axios](https://www.npmjs.com/package/axios) or any HTTP network request library you prefer as a dependency to the package. All JSON requests should be made using this library.

## Endpoints

See the [Schema Details](#SchemaDetails) section for information about the data contained in these feeds

| Feed         | URL                                                                                                       | Schema                |
| :----------- | :-------------------------------------------------------------------------------------------------------- | :-------------------- |
| Game Detail  | https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/gamedetail/[GAMEID]_gamedetail.json | [Schema](#GameDetail) |
| Play By Play | https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/pbp/[GAMEID]_[PERIOD]_pbp.json      | [Schema](#PlayByPlay) |

Examples:

- https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/gamedetail/0022000073_gamedetail.json
- https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/pbp/0022000073_1_pbp.json
- https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/pbp/0022000073_2_pbp.json
- https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/pbp/0022000073_3_pbp.json
- https://data.nba.com/data/10s/v2015/json/mobile_teams/nba/2020/scores/pbp/0022000073_4_pbp.json

## Game IDs

- 0022000073
- 0022000248 (Overtime - more than 4 periods)

## Instructions

- Create an app which takes a `gameid` command line argument
- Fetch the GameDetails json for the specified gameid.
- Use the GameDetail response to determine how many periods were played in that game, For each period, fetch the corresponding play by play file
- Once all PlayByPlay files have been received, group each of the events by `pid` (Player Id)
- write out the resulting object to a file called `./player-events.json`;

## Schema Details

### GameDetail

- **g** *{object}* - Game
  -  **mid** *{number}* - Message ID
  -  **gid** *{string}* - Game ID
  -  **gcode** *{string}* - Game Code
  -  **next** *{string}* - Next file requested
  -  **ar** *{number}* - 0 or 1, "is video archive available". Not used.
  -  **p** *{number}* - Period
  -  **st** *{number}* - Game Status (1=pregame, 2=in progress, 3=complete)
  -  **stt** *{string}* - Game Status Text
  -  **cl** *{string}* - Clock
  -  **an** *{string}* - Arena Name
  -  **ac** *{string}* - Arena City
  -  **as** *{string}* - Arena State
  -  **gdte** *{string}* - Game Date Eastern
  -  **htm** *{string}* - Game Time for Home Team
  -  **vtm** *{string}* - Game time for Away Team
  -  **etm** *{string}* - Game Time Eastern
  -  **at** *{number}* - Attendance
  -  **dur** *{string}* - Game Duration

### PlayByPlay

- **g** *{object}* - Game
  -  **mid** *{number}* - Message ID
  -  **gid** *{string}* - Game ID
  -  **gcode** *{string}* - Game Code
  -  **p** *{number}* - Period
  -  **next** *{string}* - Next file requested
  -  **pla** *{array}* - Play by play events
      - **evt** *{number}* - Event
      - **cl** *{string}* - Clock
      - **de** *{string}* - Description
      - **locX** *{number}* - Court location X
      - **locY** *{number}* - Court location Y
      - **opt1** *{number}* - Option – Event Type 1
      - **opt2** *{number}* - Option – Event Type 2
      - **mtype** *{number}* - Message Type
      - **etype** *{number}* - Event Type
      - **opid** *{string}* - Opposing player ID (e.g. for fouls)
      - **pid** *{number}* - Player ID
      - **tid** *{number}* - Team ID (of player id)
      - **hs** *{number}* - Home Team Score
      - **vs** *{number}* - Visitor Team Score
      - **epid** *{string}* - Extra Person ID
      - **oftid** *{number}* - The offensive team’s id
