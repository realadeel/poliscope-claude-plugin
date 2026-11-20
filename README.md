# Poliscope for Claude

Research US political money and influence from public records. Poliscope connects campaign finance, lobbying, federal contracts, congressional trades, votes and SEC filings across people, committees, companies and agencies, and it links answers back to the underlying records.

The plugin connects to the hosted Poliscope MCP server at `https://api.poliscope.org/mcp`. The first time you use it, you sign in to Poliscope and approve the connection. The tools only read data.

## Install

In Claude, add Poliscope from the directory. In Claude Code:

```
/plugin install poliscope --marketplace realadeel/poliscope-claude-plugin
```

## Skills

- `investigate-entity`: profile a politician, donor, company, committee or nonprofit
- `follow-the-money`: trace donations, PAC spending, lobbying, contracts and dark money
- `analyze-lobbying`: see who is lobbying whom on an issue
- `investigate-legislation`: find a bill's sponsors, funding, lobbying and votes
- `detect-conflicts`: check stock trades and donors against committees and votes
- `trace-dark-money`: follow nonprofit-to-PAC transfers and undisclosed networks
- `research-story`: check a news story or political claim against the records
- `daily-briefing`: summarize top spenders, lobbying, trades and dark money

## Support

Documentation: https://www.poliscope.org/developers
Privacy policy: https://www.poliscope.org/privacy
