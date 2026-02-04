# Title
Unprotected Admin Functionality

## Context
This write-up evaluates a PortSwigger lab demonstrating an OWASP Broken Access Control vulnerability in an administrative feature, analyzed from a development lifecycle perspective.

## What are we doing?
The application includes administrative functionality intended for authorized admin users only.

## What can go wrong?
If parts of the application intended only for administrators are accessible without server-side authorization checks, users who are not admins could access administrative features.

## How do we fix it?
Enforce role-based authorization on the server for all administrative functionality. The server must check the user’s role before allowing access, rather than relying on user interface restrictions or hidden routes.

## Did we fix it, and did we do it well?
Because the application code cannot be modified in this lab, the fix cannot be validated directly. In a real system, the fix would be considered successful if regular users attempting to access administrative functions are consistently denied, while authorized administrators retain access. Repeating this test confirms that access control is enforced on the server, not through client-side controls such as the user interface.

## Where in the lifecycle did this fail, and where should it have been caught?
The failure occurred in the Requirements phase, where access rules for administrative functionality were not explicitly defined. It continued into the Design phase, where the system did not account for enforcing role-based restrictions on the server for admin features. During Development, the design decision resulted in administrative  functionality being implemented without proper authorization checks. The issue should have been identified during Testing by verifying that users who are not admins could not access admin features through direct navigation or request manipulation. Deployment did not introduce the vulnerability, as the issue existed before release. From a Training perspective, this highlights the need for developers to understand that hiding admin functionality in the user interface does not provide absolute security. Security by obscurity is not an effective security practice.
