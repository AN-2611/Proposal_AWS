+++
title = "Check result"
date = 2022
weight = 14
chapter = false
pre = "<b>14. </b>"
+++
In this step, we will check result for Web, API, WebSocket Services then draw conclusions:
1. Web Service Test
    - **Endpoint Tested:** https://test.name.vn/
    - **Routing Rule:** Default rule forwarding to the **web-tg** Target Group.
    - **Expected Outcome:** The browser should display the static welcome page served by the NGINX web server.
2. API Service Test
    - **Endpoint Tested:** https://test.name.vn/api/
    - **Routing Rule:** Path-based rule (/api/*) forwarding to the **api-tg** Target Group.
    - **Expected Outcome:** The browser should display a JSON response from the Node.js/Express API server.
3.  WebSocket Service Test
    - **Endpoint Tested:** wss://ws.test.name.vn
    - **Routing Rule:** Host-based rule (ws.test.name.vn) forwarding to the **websocket-tg** Target Group.
    - **Expected Outcome:** A dedicated WebSocket test client should successfully establish a persistent connection and be able to send and receive messages in real-time.