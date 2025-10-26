# CSCE-606-group6-Project2
# README


This application is a Role-Based Ticket Management System built with Ruby on Rails. It enables authenticated users to create, assign, and comment on support tickets, with visibility rules and administrative controls.

## Architecture overview

### Key layers

- **Presentation (Views & Routes)**
	- Provides the UI for users to view, create, edit and manage tickets and comments.
	- Pages wire up to controller actions and present model data.

- **Controller layer**
	- Handles HTTP requests, enforces Pundit authorization and coordinates model updates.
	- Important controllers:
		- **TicketsController** — ticket lifecycle (new, create, edit, update, destroy, assign).
		- **CommentsController** — threaded/public/internal comments on tickets.
		- **UsersController** — sysadmin user management.
		- **SessionsController** — OmniAuth-based login callbacks and session lifecycle.

- **Model layer (ActiveRecord)**
	- Encapsulates business rules and associations.
		- **User** — authenticated via Google (OmniAuth); roles: `user`, `staff`, `sysadmin`.
		- **Ticket** — core entity; enums for `status` and `priority`; belongs_to `requester` and optional `assignee`.
		- **Comment** — messages attached to tickets; supports internal/public visibility.
		- **Setting** — simple key/value store used for runtime configuration (e.g., round-robin index).

- **Authorization & authentication**
	- **Authentication**: Google OAuth2 through `omniauth-google-oauth2` (test flows use OmniAuth mocks).
	- **Authorization**: Pundit policies enforce role-based permissions per resource/action.

- **Database layer**
	- Persistent storage for users, tickets, comments and settings.
	- Foreign key constraints and validations ensure referential integrity (tickets require a requester).

### Highlights

- **Round-robin auto assignment**
	- When enabled, new tickets are auto-assigned to the next staff agent tracked by `Setting` (last index).

- **Role-based access control**
	- **Requester (user)** — create tickets, view own tickets and public comments.
	- **Staff (agent)** — view assigned tickets, claim/assign and add internal comments.
	- **Sysadmin** — manage users and system settings.

- **Extensibility**
	- Designed to add new categories, notification channels or analytics with minimal changes to core models.






## Architecture & Class Diagrams

Below are the system diagrams for this project. Copy the files from your local screenshots folder into the repository (suggested path: `docs/images/`) and then view them here.

Project architecture diagram:

![Project Architecture](docs/images/project2architecture_diagram.png)

Project class diagram:

![Project Class Diagram](docs/images/project2_class_diagram.png)

<!-- If you haven't already copied the images into the repo, run the following from your machine to add them (replace paths if yours differ):

```bash
# create the images folder in the repo
mkdir -p /home/mihir/CSCE-606-group6-Project2/Ticketing-System/docs/images

# copy screenshots into the repo images folder
cp /home/mihir/Pictures/Screenshots/project2architecture_diagram.png /home/mihir/CSCE-606-group6-Project2/Ticketing-System/docs/images/
cp /home/mihir/Pictures/Screenshots/project2_class_diagram.png /home/mihir/CSCE-606-group6-Project2/Ticketing-System/docs/images/

# commit (example)
cd /home/mihir/CSCE-606-group6-Project2/Ticketing-System
git add docs/images/project2architecture_diagram.png docs/images/project2_class_diagram.png
git commit -m "Add architecture and class diagrams to README"
``` -->

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
