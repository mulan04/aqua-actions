# aqua-actions
Aqua Actions

# Aqua Image Scanner
Usage:

```[bash]
      - name: Aqua Image Scanner
        uses: mulan04/aqua-actions/Aqua_Image_Scanner@v1
        with:
            registry: registry.aquasec.com
            username: ${{ secrets.AQUA_USERNAME }}
            password: ${{ secrets.AQUA_PASSWORD }}
            scanner_image: scanner
            tag: "10"
            run_args: >-
              -v /var/run/docker.sock:/var/run/docker.sock
              -v /tmp:/tmp
              -e BUILD_URL=${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }}
              -e BUILD_NUMBER=${{ github.sha }}
            scan_args: >-
              --local aquasupportemea/insecure-bank-app:${{ github.sha }}
              --host ${{ secrets.AQUA_HOST }}
              --token ${{ secrets.AQUA_TOKEN }}
              --layer-vulnerabilities
              --jsonfile /tmp/out.json
              --htmlfile /tmp/out.html
        
      - name: Upload scan results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: Aqua Scan Report
```
Find the Aqua Scan Report in the Artifacts section of the BUILD_URL and at the configured AQUA_HOST in the CI/CD Scans tab