# DriveCare Automobile Service Management

**Enterprise service management system** — appointment booking, service time logging, multi-role access and an AI customer-support chatbot.

## Stack

Spring Boot 3.5.5, Java 21, Spring Data JPA, Spring Security/JWT, PostgreSQL · React 19.1.1, TypeScript, Tailwind, Radix · WebSocket (SockJS/STOMP), Server-Sent Events · Groq AI, Google OAuth2 · Docker Compose, CI.

## What I built

Sole developer and architect.

- **AI customer-support chatbot** (Groq API) inside a live workflow, with guardrailed prompts. It can read the booking, but it cannot write outside the tools it is given.
- **Real-time chat** between customers and staff over WebSocket, plus SSE notifications. Streaming responses, reconnect handling, and a multi-role model (Customer / Employee / Admin).
- **Appointment booking** with real-time slot availability, and service time logging for staff.
- **Auth:** Google OAuth2 social login, JWT, role-based access.

## Engineering notes

Most "AI in a product" problems are not model problems. They are permission and failure problems: what may the assistant read, what may it write, and what does the user see when the model is slow or wrong. I scoped the chatbot to read-mostly tools with explicit confirmation before any write, and made every streamed reply updatable in place so a retry does not duplicate the message.

The chat layer is deliberately transport-agnostic: the same message contract serves the WebSocket path and the REST fallback, which is what makes the reconnect logic testable.

## Code access

The repository is private because it contains client data. I can demo the booking flow, the chatbot and the real-time chat on a call, or share a recording.
