# vue-github-profile
A vue component to view the profile and repos of determined user

<img src="http://i.imgur.com/Dj7gfFd.png" alt="Demonstração economist">

## Instalation
```sh
$ npm install --save vue-github-profile
```

## Usage

```HTML
<GithubProfile width="width" user="github-user"></GithubProfile>
```

```javascript
<script>
import GithubProfile from 'vue-github-profile'

export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    GithubProfile
  }
}
</script>
```

## Example

```HTML
<GithubProfile width="20em" user="gabrielbibiano"></GithubProfile>
```
