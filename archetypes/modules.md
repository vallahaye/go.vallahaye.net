{{- $baseURL := urls.Parse .Site.BaseURL -}}
{{- $module := path.Join $baseURL.Host (strings.TrimPrefix "modules/" .Dir) .Name -}}
{{- $import := getenv "HUGO_MODULE_ARCHETYPE_IMPORT" -}}
{{- $source := getenv "HUGO_MODULE_ARCHETYPE_SOURCE" -}}
{{- $repoURL := getenv "HUGO_MODULE_ARCHETYPE_REPO_URL" -}}
---
module: "{{ $module }}"
import: "{{ $module }} {{ delimit (split $import " " | after 1) " " }}"
source: "{{ with $source }}{{ $module }} {{ delimit (split . " " | after 1) " " }}{{ end }}"
repoURL: "{{ $repoURL }}"
---

