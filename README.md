# 648-Assignment1

Some main takeaways:
1. I'm a full time software engineer (Rails/React)
2. I'm a tad worried this class might be too high level for me but excited to learn and go deeper
3. I'm excited to be admitted into the SDSU M.S. Computer Science program!

Some websites I've built in the past using frameworks such as GatsbyJS (a wrapper around React)
* [My photography Site](https://garretthughesphotography.com/)
* [My web dev site](https://garrett-hughes.com/)

***

## Here are some of my pictures:

### My Dog, `Roxy`:
![Roxy](https://garretthughesphotography.com/static/f589e3cef4d6689a5d2842815622b626/7e193/roxy-personal-hiking-cover.webp "Roxy")

### One of my favorite images:
![Roxy](https://garretthughesphotography.com/static/baf3deca92e531da242e72d3a963fd37/7e193/astro-photography-nightscape-cover.webp "Roxy")

Bonus round... here is an authentication service I wrote today!
```
import ServerApi from '../utils/apis/ServerApi'
import { navigate } from 'gatsby'

export const isBrowser = () => typeof window !== 'undefined'

const asyncLocalStorage = {
  setItem: function(key, value) {
    return Promise.resolve().then(function() {
      localStorage.setItem(key, value)
    })
  },
  getItem: function(key) {
    return Promise.resolve().then(function() {
      return localStorage.getItem(key)
    })
  },
}

export const getJWT = () =>
  isBrowser() && window.localStorage.getItem('jwt')
    ? JSON.parse(window.localStorage.getItem('jwt'))
    : {}

export const setJWT = (jwt, redirect) => asyncLocalStorage.setItem('jwt', JSON.stringify({ jwt: jwt })).then(() => {
  navigate(redirect)
})

export async function validateJWT() {
  await ServerApi.authenticateToken(getJWT()).then(() => {
    return true
  }).catch(() => {
    return false
  })
}

export const isLoggedIn = () => {
  const user = getJWT()

  return !!user.username
}

export const logout = () => {
  setJWT({}, '/admin/login')
}
```
