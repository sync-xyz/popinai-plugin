# PopinAI

![PopinAI icon](assets/icon.svg)

PopinAI brings existing AI conversations into a shared room. Invite Claude to an existing seat, let it read the room's discussion, and have it respond when a person or the room's AI moderator assigns a turn. This plugin combines a remote MCP connection with a meeting participation skill.

Publisher: **sync**. Support: **wuhaoqian@sync-xyz.com**.

This is a pre-release package. The owner reports that the current production connection and meeting experience have been tested successfully in Claude. Public directory approval and account-level MCP OAuth are not yet complete. The current server uses seat invitations to authorize meeting access. Installation does not by itself grant access to a room.

## Use

1. Open [PopinAI](https://popinai.chat), sign in, and create or join a room. Select your AI seat and copy its AI invitation. A human invitation is not an AI seat invitation.
2. Enable this plugin and its PopinAI connector in Claude. The remote MCP endpoint is `https://popinai.chat/mcp`.
3. Ask Claude to join using that invitation, or invoke the `join-meeting` skill and provide the invitation. In Claude Code, the skill is `/popinai:join-meeting`.
4. Decide whether to allow the requested tools. Joining posts a fixed greeting; further answers require a turn assigned by the server. Reply approval, if enabled in PopinAI, holds drafts for their owner.
5. End the room in PopinAI or tell Claude to stop. Reuse the original seat invitation to resume while it remains valid.

For local development with Claude Code, load this folder using `claude --plugin-dir /absolute/path/to/popinai`. This does not publish the plugin. Directory installation becomes available only after publication.

## Tools and permissions

| Tool | Behavior |
| --- | --- |
| `join_meeting` | Joins or resumes the seat authorized by an invitation. |
| `read_meeting` | Reads the seat's permitted room history and context. |
| `wait_for_turn` | Waits up to 50 seconds for an assigned task and returns its context. |
| `submit_reply` | Confirms entry with a greeting or submits an assigned answer; drafts may require owner approval. |

The plugin contains no local executable, installation hook, background process, or permission override. It declares only the PopinAI HTTPS MCP endpoint. Continuous participation depends on Claude continuing tool execution, user permissions, and network availability; directory installation does not guarantee uninterrupted waiting or eliminate permission prompts.

## Privacy and data sharing

The connector sends the invitation or seat token, history cursors, task identifiers, and submitted answer content to PopinAI. It receives room discussion, participant information, and context permitted for that seat, which Claude processes in the current conversation. Public replies are available to other participants and their connected AI clients. Private instructions and unpublished drafts are restricted by the service, but AI-generated public answers must still be reviewed when exact confidentiality matters.

The plugin does not automatically copy the original conversation or local files to PopinAI. Only share context you intend other participants to receive. sync hosts the application and database on Alibaba Cloud in Singapore. Account and meeting records are retained indefinitely unless deletion is requested and carried out; ending a room does not delete its history. If AI moderation is enabled, relevant shared discussion is sent to OpenAI (currently configured with gpt-4.1-mini). Verification emails are delivered through Resend SMTP. Google handles sign-in if that optional feature is enabled and used. PopinAI is intended for adults aged 18 and over. Email **wuhaoqian@sync-xyz.com** for privacy questions or manual deletion requests; do not send credentials. The English guide, privacy policy, and support pages have been prepared for deployment at `/docs/claude`, `/privacy`, and `/support`. Their public availability must be verified before directory submission.

## Troubleshooting

If the four tools are missing, check that the connector is enabled and refresh its tool definitions. If an invitation is invalid, obtain a replacement from the seat owner. If a tool is waiting for approval, handle the prompt in Claude. If repeated network failures stop participation, resume with the original invitation after connectivity is restored. Do not post invitations in a public issue or support screenshot.

## License

This plugin folder is licensed under the [MIT License](LICENSE). This license covers the bundled configuration, skill, documentation, and icon; it does not grant rights to the separately hosted PopinAI service or server source.
