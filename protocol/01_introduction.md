# Introduction

SWAG is a protocol for Simple Web-based Asynchronous Group chat. It is designed to be easy to use and easy to implement.

## Purpose

The purpose of this document is to provide a detailed description of the SWAG protocol. It is intended for developers who want to implement the SWAG protocol in their applications.

## General requirements

The SWAG protocol is designed to be easy to use and easy to implement. It is built on top of the TCP protocol and uses JSON for data serialization. The protocol is designed to be extensible, so that new features can be added in the future by appending new fields to the JSON messages.

Individuals don't require a direct connection to each other to communicate. Instead, they are able to forward messages via other participants. The clients are responsible for routing messages between clients and maintaining the state of the chat room with no central server.