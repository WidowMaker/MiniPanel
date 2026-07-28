# Vejrudsigt til MiniPanel Dashboard

Sådan tilføjer du en vejrudsigt-side med et hurtigt-access-knap på hjem-skærmen.

## 1. krav

Installer disse HACS custom cards:
- [button-card](https://github.com/custom-cards/button-card)
- [weather-forecast-card](https://github.com/bramkragten/weather-forecast-card) (eller `custom:weather-forecast` hvis det allerede er installeret)

---

## 2. Vejr-knap på Home-skærmen (pille)

Tilføj dette som `custom_field` i dit home-kort. Det viser et lille "Vejrudsigt"-knap ved siden af vejret.

### Tilføj custom_field `weather_pill`:

```yaml
weather_pill:
  type: custom:button-card
  show_icon: false
  show_name: false
  show_state: false
  tap_action:
    action: navigate
    navigation_path: /dashboard-minipanel/vejr
  custom_fields:
    pill: "[[[return `<div style=\"display:flex;align-items:center;gap:6px;color:#F4F6F2;font-size:13px;font-weight:850;white-space:nowrap;\"><ha-icon icon=\"mdi:weather-partly-cloudy\" style=\"width:18px;height:18px;color:#F4F6F2;\"></ha-icon> Vejrudsigt</div>`;]]]"
  styles:
    card:
      - width: auto
      - height: 38px
      - border-radius: 999px
      - padding: 0 14px
      - background: rgba(18, 21, 30, 0.68)
      - border: 1px solid rgba(247, 248, 244, 0.14)
      - box-shadow: 0 6px 14px rgba(0, 0, 0, 0.18)
      - cursor: pointer
    custom_fields:
      pill:
        - display: flex
        - align-items: center
        - justify-content: center
```

### Positioner pillen (i `styles.custom_fields`):

```yaml
styles:
  custom_fields:
    weather_pill:
      - position: absolute
      - left: "calc(50% + 85px)"
      - top: "50%"
      - transform: translateY(62px)
      - z-index: 8
```

---

## 3. Vejrudsigt-side

Tilføj en ny view i dit dashboard:

```yaml
- path: vejr
  title: Vejr
  icon: mdi:weather-partly-cloudy
  cards:
    - type: custom:button-card
      show_icon: false
      show_name: false
      show_state: false
      triggers_update:
        - weather.forecast_home
        - sensor.udendors_temperatur
      custom_fields:
        idle_return: "[[[\n  if (!window.minipanelIdleReturnInstalled) {\n    window.minipanelIdleReturnInstalled = true;\n    const timeout = 60000;\n    const returnPath = '/dashboard-minipanel/home';\n    let timer;\n    const resetTimer = () => {\n      clearTimeout(timer);\n      timer = setTimeout(() => {\n        const path = window.location.pathname;\n        const search = window.location.search || '';\n        if (\n          path.startsWith('/dashboard-minipanel') &&\n          !search.includes('disable_km') &&\n          path !== '/dashboard-minipanel/home'\n        ) {\n          history.pushState(null, '', returnPath);\n          window.dispatchEvent(new Event('location-changed'));\n        }\n      }, timeout);\n    };\n    ['click', 'touchstart', 'mousemove', 'keydown'].forEach(eventName => {\n      document.addEventListener(eventName, resetTimer, true);\n    });\n    resetTimer();\n  }\n  return '';\n]]]"
        back:
          type: custom:button-card
          icon: mdi:arrow-left
          show_icon: true
          show_name: false
          show_state: false
          tap_action:
            action: navigate
            navigation_path: /dashboard-minipanel/home
          styles:
            card:
              - width: 50px
              - height: 50px
              - border-radius: 50%
              - padding: 0
              - margin: 0
              - box-shadow: none
              - background: rgba(18, 21, 30, 0.82)
              - border: 1px solid rgba(247, 248, 244, 0.14)
            icon:
              - width: 26px
              - height: 26px
              - color: "#F4F6F2"
        weather:
          type: custom:button-card
          entity: weather.forecast_home
          show_icon: false
          show_name: false
          show_state: false
          custom_fields:
            weather_card:
              type: custom:weather-forecast
              entity: weather.forecast_home
              forecast_type: daily
              number_of_forecasts: 5
              show_forecast: true
              animations: true
              color: "#F4F6F2"
          styles:
            card:
              - width: 100%
              - padding: 16px
              - border-radius: 22px
              - background: rgba(18, 21, 30, 0.82)
              - border: 1px solid rgba(247, 248, 244, 0.14)
              - box-shadow: 0 6px 14px rgba(0, 0, 0, 0.22)
            custom_fields:
              weather_card:
                - width: 100%
        menu:
          type: vertical-stack
          cards:
            - icon: mdi:home-outline
              tap_action:
                action: navigate
                navigation_path: /dashboard-minipanel/home
              template: minipanel_menu_button
              type: custom:button-card
            - icon: mdi:lightbulb-outline
              tap_action:
                action: navigate
                navigation_path: /dashboard-minipanel/lys
              template: minipanel_menu_button
              type: custom:button-card
            - icon: mdi:thermometer
              tap_action:
                action: navigate
                navigation_path: /dashboard-minipanel/klima
              template: minipanel_menu_button
              type: custom:button-card
            - icon: mdi:speaker
              tap_action:
                action: navigate
                navigation_path: /dashboard-minipanel/musik
              template: minipanel_menu_button
              type: custom:button-card
            - icon: mdi:home-automation
              tap_action:
                action: navigate
                navigation_path: /dashboard-minipanel/status
              template: minipanel_menu_button
              type: custom:button-card
      extra_styles: ""
      styles:
        card:
          - height: 100vh
          - width: 100vw
          - padding: 0
          - margin: 0
          - border-radius: 0
          - border: 0
          - box-shadow: none
          - overflow: hidden
          - position: relative
          - background-image: 'url("/local/minipanelbackground.png")'
          - background-size: cover
          - background-position: center center
          - background-repeat: no-repeat
        custom_fields:
          back:
            - position: absolute
            - left: 34px
            - top: 36px
            - z-index: 9999
          weather:
            - position: absolute
            - left: 34px
            - right: 174px
            - top: 100px
            - bottom: 36px
            - z-index: 3
          menu:
            - position: absolute
            - right: 18px
            - top: 36px
            - width: 96px
            - padding: 12px 8px
            - border-radius: 30px
            - background: rgba(12, 15, 24, 0.92)
            - border: 1px solid rgba(247, 248, 244, 0.14)
            - box-shadow: 0 8px 16px rgba(0, 0, 0, 0.24)
            - z-index: 9999
            - display: flex
            - align-items: center
            - justify-content: center
        grid:
          - height: 100vh
          - width: 100vw
          - display: grid
          - grid-template-areas: '"weather"'
          - grid-template-columns: 1fr
          - grid-template-rows: 1fr
      type: custom:button-card
  type: panel
```

---

## 4. Udskift entity IDs

Erstat følgende med dine egne:

| I guiden | Din entity |
|----------|------------|
| `weather.forecast_home` | Dit weather-entitity |
| `sensor.udendors_temperatur` | Din udendørs temperatur-sensor |

---

## 5. Menu-knapper (valgfrit)

Hvis du ikke bruger `minipanel_menu_button` template, skal du erstatte alle `template: minipanel_menu_button` med fulde menu-kort-definitioner. Se eksisterende views for mønster.

---

## 6. idle_return

Koden i `idle_return` sender brugeren tilbage til home efter 60 sekunders inaktivitet. Fjern feltet hvis du ikke vil have denne funktion.
