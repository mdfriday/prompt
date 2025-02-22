{{ define "main" }}

{{ template "before-tasking.md" . }}

{{ .Content "prompts/tasking.md" }}

{{ template "after-tasking.md" . }}

{{ end }} 