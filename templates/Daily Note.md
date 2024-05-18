## Daily retrospective
### Achievements and events
- 
### What did I learn today?
- 
### What could have made today better?
- 

## Log
## Notes
## Agenda
<%*
const {getEvents} = this.app.plugins.plugins["google-calendar"].api;
const theEvents = await getEvents({startDate: window.moment()});

theEvents.forEach(({summary, start, hangoutLink, recurringEventId, attendees, description}) => {
	const eventBlacklist = /(via Scoop|Meeting Room)/g;
	if(!summary || summary.match(eventBlacklist)) return;
	if(attendees && attendees.findIndex(({ self, responseStatus }) => self && responseStatus === "accepted") === -1) return;
	if(start.dateTime) {
		const time = moment(start.dateTime);
		const timeString = time.format('LT')
		const dateString = time.format('YYYY-MM-DD')
		const title = summary.replace('/', '-')
		const obsidianLink = recurringEventId ? `[[Meeting Notes/recurring/${title}#${dateString}|${title}]]` : `[[Meeting Notes/one-offs/${title}#${dateString}|${title}]]`
		tR += 
`### ${timeString} - ${title}
[Google Meet](${hangoutLink})
${obsidianLink}
!${obsidianLink}
`;
	}
})
%>