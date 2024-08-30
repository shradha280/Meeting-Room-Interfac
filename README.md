# Meeting-Room-Interfac
Hight level design
Block diagram 
+----------------+        +----------------+        +-----------------+
|                |        |                |        |                 |
| Meeting        |        | Participant    |        | Meeting Room    |
| Scheduler      +--------+ Manager        +--------+ Manager         |
|                |        |                |        |                 |
+----------------+        +----------------+        +-----------------+
        |                        |                        |
        |                        |                        |
        v                        v                        v
+----------------+        +----------------+        +-----------------+
|                |        |                |        |                 |
| Meeting        |        | Participant    |        | Meeting Room    |
| Database       |        | Database       |        | Database        |
|                |        |                |        |                 |
+----------------+        +----------------+        +-----------------+

--- Meeting Scheduler interacts with Meeting Manager, Participant Manager, and Meeting Room Manager to schedule meetings and check for conflicts.
--- Database for storing meeting, participant, and room data.


Flow - 
Scheduling a Meeting:

--- User requests to schedule a meeting with date, time, participants, and room.
--- System checks if the meeting room is available and if all participants are free.
--- If no conflicts, the meeting is scheduled and data is stored.

Detecting Conflicts:

-- Before scheduling, the system checks the availability of the meeting room and participants.
-- If conflicts are found, the user is notified.


Schema Design
Tables 
1. Meetings
id (INTEGER, Primary Key)
title (VARCHAR)
start_time (DATETIME)
end_time (DATETIME)
room_id (INTEGER, Foreign Key)

2. Participants
id (INTEGER, Primary Key)
name (VARCHAR)
MeetingParticipants
meeting_id (INTEGER, Foreign Key)
participant_id (INTEGER, Foreign Key)

3. Rooms
id (INTEGER, Primary Key)
room_name (VARCHAR)


Endpoint - POST /scheduleMeeting

Request Body - 
{
  "title": "Project Sync",
  "start_time": "2024-09-01T10:00:00Z",
  "end_time": "2024-09-01T11:00:00Z",
  "room_id": 1,
  "participants": [1, 2, 3]
}

Response Body - 
    {
  "status": "success",
  "message": "Meeting scheduled successfully",
  "meeting_id": 123
}

Endpoint - GET/checkl Availability

Request Parameters - 

{
        start_time: "2024-09-01T10:00:00Z"
        end_time: "2024-09-01T11:00:00Z"
        room_id: 1
        participants: [1, 2, 3]
}

Reponse 
{
  "status": "available",
  "conflicts": {
    "rooms": [],
    "participants": []
  }
}






