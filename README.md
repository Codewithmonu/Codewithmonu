- 👋 Hi, I’m @Codewithmonu
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Codewithmonu/Codewithmonu is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
jobs:
  notify-irc:
    runs-on: ubuntu-latest
    steps:
      - name: irc push
        uses: rectalogic/notify-irc@v1
        if: github.event_name == 'push'
        with:
          server: irc.hackthissite.org
          port: 7000
          tls: true
          notice: true
          channel: "#ctf"
          nickname: GitHub
          message: |
            ${{ github.actor }} pushed ${{ github.event.ref }} ${{ github.event.compare }}
            ${{ join(github.event.commits.*.message) }}
      - name: irc pull request
        uses: rectalogic/notify-irc@v1
        if: github.event_name == 'pull_request'
        with:
          server: irc.hackthissite.org
          port: 7000
          tls: true
          notice: true
          channel: "#ctf"
          nickname: GitHub
          message: |
            ${{ github.actor }} opened PR ${{ github.event.html_url }}
      - name: irc tag created
        uses: rectalogic/notify-irc@v1
        if: github.event_name == 'create' && github.event.ref_type == 'tag'
        with:
          server: irc.hackthissite.org
          port: 7000
          tls: true
          notice: true
          channel: "#ctf"
          nickname: GitHub
          message: |
            ${{ github.actor }} tagged ${{ github.repository }} ${{ github.event.ref
