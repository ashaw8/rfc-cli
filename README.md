# rfc

Read IETF RFCs and Internet-Drafts from the terminal, and follow the IETF meeting agenda.

A single Python 3 script using only the standard library: no pip, no dependencies.

## Install

Clone this repository and link the script onto your `PATH`:

```sh
ln -s "$PWD/rfc" ~/.local/bin/rfc
```

Requires Python 3.9+ (`zoneinfo`) and a pager (`less` by default; override with `RFC_PAGER` or `PAGER`).

## Usage

### RFCs and drafts

```sh
rfc 9000                         # read RFC 9000 in less
rfc 9000 -s "Packet Protection"  # open and jump to the first match
rfc info 793                     # status, authors, obsoletes / obsoleted-by / updates, abstract
rfc search quic congestion       # search titles, keywords, abstracts (-a includes obsoleted RFCs)
rfc draft quic-multipath         # latest revision of draft-ietf-quic-multipath
rfc draft draft-foo-bar-07       # a specific revision
rfc wg quic                      # a working group's active drafts and published RFCs
rfc get 9000 9001 9002           # pre-fetch for offline reading
rfc ls                           # what's cached locally
rfc sync                         # refresh the RFC index (also refreshes itself weekly)
```

Reading an obsoleted RFC prints a note pointing at its replacement. Output is plain text when piped,
so `rfc 9000 | grep -n MUST` works.

### IETF meeting agenda

Defaults to the current or most recent meeting; add a number (e.g. `rfc ietf 126 quic`) for another.

```sh
rfc ietf                  # full schedule: ▶ in progress, ★ starred, past sessions dimmed
rfc ietf now              # in progress or starting within 90 minutes
rfc ietf today | tomorrow | wed
rfc ietf quic             # a WG's sessions, rooms, Meetecho/notes links, posted agenda, slides,
                          # and the drafts named on its agenda
rfc ietf sec              # all sessions in an area
rfc ietf star quic tls    # follow WGs; `rfc ietf mine` shows just those
```

Times are shown in the meeting's local time zone.

## Data sources and caching

- RFC index and text: <https://www.rfc-editor.org>
- Drafts, working groups, meeting agendas: the [IETF Datatracker](https://datatracker.ietf.org) API

Everything fetched is cached in `~/.cache/rfc` (respects `XDG_CACHE_HOME`), so documents you've opened
once stay readable offline. The meeting agenda is refreshed at most hourly, falling back to the cached
copy when offline. Starred WGs are stored in `~/.config/rfc/starred`.

Set `NO_COLOR=1` to disable colors.

## License

MIT. See [LICENSE](LICENSE).
