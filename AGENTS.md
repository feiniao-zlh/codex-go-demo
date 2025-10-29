# Repository Guidelines

## Project Structure & Module Organization
This Go service lives at the repository root. `main.go` wires the Gin router and serves as the entry point. Dependencies are tracked in `go.mod` and `go.sum`. When extracting reusable handlers or middleware, place them under `internal/server/...`; public packages belong under `pkg/...`. Mirror source layout in tests, e.g. `internal/server/handler_test.go`.

## Build, Test, and Development Commands
Use `go run .` for local development; it starts the Gin server on `:8080`. `go build` compiles the project into a binary in the current directory. `go test ./...` executes the full test suite, and adding `-race` helps surface concurrency bugs. Run `go mod tidy` after adding or removing dependencies to keep the module graph clean.

## Coding Style & Naming Conventions
Rely on `gofmt` (or `go fmt ./...`) and `goimports` before committing. Follow idiomatic Go naming: exported symbols use PascalCase only when they must be shared; keep handlers and middleware unexported unless required externally. Group Gin routes by feature and prefix with the HTTP verb, e.g. `router.GET("/health", ...)`. Prefer structured logging via `log.Printf` or a shared logger helper.

## Testing Guidelines
Write unit tests with Go’s `testing` package and exercise Gin handlers using `httptest`. Name test files with the `_test.go` suffix and test functions `TestXxx`. Target at least 80% coverage for new logic and favor table-driven tests for route edge cases. Run `go test -cover ./...` before pushing changes.

## Commit & Pull Request Guidelines
Craft commit subjects in imperative mood (e.g., `Add auth middleware`) and keep them under roughly 65 characters. Reference issue IDs in the body when applicable. Pull requests should outline the change, tests performed, and any new routes or environment variables. Attach screenshots or curl snippets when HTTP responses change.

## Security & Configuration Tips
Never commit secrets; load configuration via environment variables at runtime. Document new configuration keys in the README and validate them during startup.
