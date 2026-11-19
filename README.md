# Quantum Relay

**Construct the global network, connection by connection.** A complimentary, illustrated browser-based simulation detailing the mechanics of modern internet infrastructure. Accessible via **[github.com/Ha1381Di](https://github.com/Ha1381Di)**.

![Quantum Relay]

Begin your operations with a solitary routing node in a single metropolitan area and scale your enterprise until you operate a transit-free Tier 1 network:

- **Client Base:** Acquire residential broadband subscribers, corporate entities, hosting providers, L2VPN clients, and DDoS mitigation services. Cater to high-frequency trading firms with strict latency requirements, AI GPU data centers, and hyperscaler DCI agreements. Note that some clients demand very specific operational prerequisites.
- **Network Interconnection:** Manage IP transit billing based on 95th-percentile usage. Utilize internet exchanges with route servers, and negotiate open, selective, restrictive, or paid peering arrangements. Deploy Private Network Interconnects (PNIs), embedded CDN caching, and NNI fabrics for virtual circuits and remote peering.
- **Physical Infrastructure:** Lease wavelengths across approximately 40 geographically accurate subsea cable systems. Utilize leased or self-constructed dark fiber, illuminated with DWDM and ZR+ optics. Upgrade router hardware generations to increase maximum port speeds, and implement Link Aggregation Groups (LAGs) to bundle capacity when a single port is insufficient.
- **Traffic Management:** Analyze real-time link utilization, adjust link metrics, and configure egress preferences. Direct high-frequency trading traffic through the fastest available routes while routing backup data through more scenic, less congested paths.
- **Operational Disruptions:** Face constant threats including physical cable excavation, shark bites, human error, BGP route leaks, RPKI validation failures, DDoS assaults, cooling system failures, geopolitical cable severances, and mandated internet shutdowns.
- **Multiplayer Integration:** Engage with other operators on community-hosted servers. Negotiate peering agreements, trade transit and wavelengths, collaborate on cable construction, and compete on live global leaderboards. This feature is entirely optional and can be toggled per save file without affecting solo gameplay.

All corporate entities within the game are satirical puns; no actual company names are utilized. The game requires no account registration or cookies: the [privacy policy](https://github.com/Ha1381Di/privacy.html) details exactly what local data is stored on your device, what data is transmitted to Multimode servers, and what is retained by those servers.

## Educational Value

This simulation simplifies complex networking concepts and intentionally exaggerates certain aspects for comedic effect. To understand the real-world mechanics, we recommend exploring interactive, zoomable maps that trace data from local Wi-Fi through copper and undersea fiber across different eras of the internet (1995, 2010, and today). Engaging with these technical resources for an hour will provide more genuine insight than a year of laying cartoon fiber here.

## Multiplayer: Network with Others

Activate the **Multiplayer** feature when establishing a new network, or join later via the Multimode menu. Other players' networks will appear as destination points for your clients, allowing you to negotiate peering, transit, PNIs, exchange ports, wavelengths, capacity swaps, and consortium cables. All transactions are end-to-end encrypted, preventing servers from reading the details. Live leaderboards update every 30 seconds to rank traffic volume, Points of Presence (POPs), profitability, and customer cone size.

The primary server, **Quantum Relay Server 1** (`wss://s1.yourdomain.com/fed`), is publicly accessible. Additional servers will appear in-game as the community deploys them. If a server goes offline, your local game will continue to function normally.

## Local Deployment

The game operates as a single static webpage, compiled from the `src/` directory by a lightweight Node script. Progress is automatically saved to your browser's local storage. For testing multiplayer on mobile devices, run the HTTPS command to generate a secure connection and follow the certificate trust instructions.

```sh
npm install
npm run dev                   # Launches local development server at http://localhost:8080
The interface supports English, Italian, Portuguese, French, Spanish, and German. It automatically detects your browser's language upon first launch and remembers your manual selection via the settings menu.

Server Hosting
Multiplayer relies on community-hosted servers: a lightweight Go program that relays signed records between games. It never accesses player strategies or financial data, does not log IP addresses, and operates efficiently on a small VPS or Raspberry Pi.

For public hosting, you will need a static IP, a registered domain, open ports (80/443), and a valid TLS certificate. Deployment is streamlined via Docker Compose:

sh
git clone https://github.com/Ha1381Di/quantum-relay.git
cd quantum-relay/relay
cp .env.example .env        # Configure RELAY_DOMAIN, LETSENCRYPT_EMAIL, and RELAY_NAME
docker compose up -d --build
docker compose logs -f relay
First startup initializes the server, provisions the certificate, and generates an operator key. Ensure you back up this key immediately, as there is no recovery method.

Server Listing: Submit a pull request with a signed registry file to appear in the in-game server list. Listed open servers automatically sync.

LAN Parties: Local networking requires no domain. Run the LAN command to generate a self-signed certificate, allowing local devices to join without internet access.

Alternative Deployment: Static binaries and container images are available for major operating systems and architectures.

Monitoring: Prometheus metrics and a Grafana dashboard are included for operational oversight.

Comprehensive step-by-step guides for Docker, systemd binaries, upgrades, and backups are available in the documentation directory.

Development Workflow
Use the provided scripts for development, testing, building, translation checks, and performance benchmarking.

sh
npm install
npm run dev    # Assembles src/ on request, auto-reloads on save
npm test       # Executes headless test suites (geography, simulations, incidents)
npm run build  # Generates static site for GitHub Pages deployment
npm run i18n:check  # Validates translation completeness
npm run mcp    # Exposes game state via MCP server for AI integration
npm run perf -- --base-ref origin/main   # Benchmarks large network performance
node scripts/fed-e2e.js --quick          # End-to-end multiplayer simulation
(cd relay && go test ./...)              # Executes relay server unit tests
Detailed architecture and federation protocols are documented in the docs/ directory.

Community and Contributions
Share your network screenshots, suggest new metropolitan areas, and debate peering policies with other operators. Please direct any bug reports or feature requests to the GitHub issue tracker. All contributors are expected to adhere to the Code of Conduct.