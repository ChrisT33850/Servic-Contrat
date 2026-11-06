# Crée ou édite README.md
cat >> README.md << 'EOF'

## Payment Link Project Flow

```mermaid
flowchart TD
    A["Asset créé<br/>Garantie initiale = 24 mois"] --> B{"PM Required ?"}

    B -->|Non| C["Garantie maintenue<br/>24 mois"]
    B -->|Oui| D["Contrôle Salesforce<br/>PM réalisée dans les 12 mois<br/>suivant la vente ?"]
    D -->|Oui| E["Garantie maintenue<br/>24 mois"]
    D -->|Non| F["Garantie réduite<br/>à 12 mois"]

    C --> G["Client clique sur<br/>Warranty Extension"]
    E --> G
    F --> G

    G --> H{"PM Required ?"}
    H -->|Non| I["Extension autorisée"]
    H -->|Oui| J["Recherche Salesforce<br/>de la dernière Preventive<br/>Maintenance"]

    J --> K{"PM trouvée ?"}
    K -->|Oui| M{"PM End Date<br/>>= date de la demande ?"}
    K -->|Non| L

    M -->|Oui| I
    M -->|Non - PM expirée| L

    L["Proposition par défaut :<br/>Extension de garantie AVEC PM<br/>(PM incluse dans l'offre)"] --> N{"Client accepte<br/>l'offre avec PM ?"}
    N -->|Oui| O["Extension autorisée<br/>+ PM ajoutée / planifiée"]
    N -->|Non| P["Extension refusée"]

    style I fill:#90ee90
    style O fill:#90ee90
    style C fill:#90ee90
    style E fill:#90ee90
    style F fill:#ffb3b3
    style P fill:#ffb3b3
    style L fill:#ffd9a0
    style N fill:#ffd9a0
```


EOF

git add README.md
git commit -m "Add Payment Link flowchart to README"
git push origin main
