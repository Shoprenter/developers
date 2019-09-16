# Dokumentáció csatolása termékhez

Az alábbi példában bemutatásra kerül, hogy miként lehet a ShopRenter API-n keresztül fájlt feltölteni és azt a kiválasztott termékhez csatolni.

## 1. lépés

A [File resource](https://www.shoprenter.hu/api/doc#file) segítségével töltsük fel a kívánt dokumentumot (pl. egy képet). Fontos, hogy a request **body**-ban megadott **filePath** értékének adjuk meg a `srattached\/` mappát, illetve a **type** értéke mindenképp `image` legyen.

### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/files</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": {
        "filePath": "srattached\/image.jpg",
        "type": "image",
        "attachment": "JVBERi0xLjQKJcOkw7zDtsOfCjIgMCBvYmoKPDwvTGVuZ3RoIDMgMCBSL0ZpbHRlci9GbGF0ZURlY29kZT4+CnN0cmVhbQp4nC2JuwqDQBBF+/mKW6dY76i7s4IEotFeGMgP5AEpAtrk9zNFuMU9nMOk+MoOxvKQU4vaa6o4HnI74fMvxPGSySWXSGYlGfyOZlUo4c+RypYde2aWeAuqYSx44IUTZ17P/pbFZZMNP6GRGJQKZW5kc3RyZWFtCmVuZG9iagoKMyAwIG9iagoxMDgKZW5kb2JqCgo1IDAgb2JqCjw8L0xlbmd0aCA2IDAgUi9GaWx0ZXIvRmxhdGVEZWNvZGUvTGVuZ3RoMSA5NjQ4Pj4Kc3RyZWFtCnic5Th5eBPXnb83Mzpt6/CFsYAZIeyY+JBtYRIo4MG2hMEGC2wHCQi2bMmWEltSJJmraTE5wZwpNEdDN2nS5iBJGUOzmIQF2nTzJd+SJl+aft1u6ULTtNtuDrJpku0R5P29p7Ex5Phjv/1vR3rzfu93X+9pRqnEUAiyYRh4kHsHA/EaW1EuAJwDILm9m1JSX1RwIXwRgPthX7x/8DsnNnwMIBwA0P2of2Br3w3P/+4/AbKbcH0gHAoEF/TdVwOQ9xbqmB9GxMOXj2gB8rNxPSc8mNryMf86XVfjevZArDdQaP4QafkddD0Y2BJ/WFjC43oLrqVoYDAUaBtC3vwHAbK2xmPJVAeUppGUT+nxRCj+waFPuhGcB6DZhjiCH3qhTqKla44XNFqd3mDMMZnh/+GlOac5B9/QuKEAutn9qktYCPmwGWD8Pboaf2+8KwOn16bX/l96oc9MP4J/giPwKLyC0N0qaSd8E34AZ69iPwOvwjOwB07Bw7AX5n2p2pOo53YGHYKuL7dOnoIYbIHvo907Ud+LsJGMEB66IQU7YAxte4VR4aV0K7xLjsFLxABfJ+Xc/ejD/fBrzb8Kv/icwm/BU3Ar3k/g/WGK4D6Cb3FLIMr9gHfDLoywm2tF9EtoexV8n6yHjbjDIugFIBS+SlcpvwLuha8jNDSVornjs1HIGv8YPd4F+9GTCNwG62GNSj7G4S6BvbyI0fwQnme43ROy2qf5OHeK019+CO7Dz0r8BCFIdsAj8FQ6nD4MDxM3ccOB9Kfjf4JtGje3ErLHP9A8+NmfIQqt0AMe+OOXZ1P17xyYP5s1/hH3dzAJhWBM/xyrpl78erBcno3dtGX8w3R3uh15zEKh5geaY5qXYCt0aXcIYcgX/oV13M/T2zHGX2NfvIB5A3nZ+nV+X2dH+5rV3rZVK1tbVixvXuZxNzU2LJXrlyxe9LWFC268YX5dTbWzqrKi7LrSkjmO2XaxKN9qMZtysowGvU6rEXiOQIWkkG63wpdIVk/A4XYEmisrJHdRuKmywu3wdCtSQFJwEkodzc0M5QgoUreklOIUmILuVmTk7LuGU85wypOcxCItgkXUhENSXmtySGNk3WofwnubHH5JeZ/BKxkslLJFDi7sdpRgXlFvJbfi2RQecXejj2Q0y9joaAwZKytg1JiFYBZCSpkjPkrKlhAGcGXuhaMc6HOoWYzUHQgq3tU+d5PNbvdXVixXTI4mRoJGplLRNio6plKKUNdhtzRacXZkz5gFerrLs4OOYGCDT+EDKDvCu0dG7lWs5cpcR5Myd9s7RRh5SKlwNLmVcqq1Zc2knZYrJomiKbE4pJFPAMNxvP/e1ZiAitGWWD4BCipco0LW+Oz0snkw1yMjHofkGekeCYyND/c4JItjZDQ7eyTuxnSD14cqxsZf2G1TPHv8iqU7TBb61dA9a1qUvNXrfQpX4pHCAcTgt95hv9Fmt07yeL+MDJgWTA5m2G6nadg9JkMPLpTh1b7MWoIe2zGQneV+heumlLMTlIJOShmeoEyKdzuwti3tvhFFKFkedLgx47sDynAPdtcttDAOi2L61GZ3jORapQVOP+OV0KvlwYikaEoxSSg1VQD7hoqMWNjC9Glmet+GBkqtudICB6qhetwOd7f63RQuQgUSJrq5PNMIHT5FbkJADqgVc49WO1Ei0I0FizSxYipOR1zJdzRMVpe65Y60+5iIKqbkNyrQ3atKKU4321eSe6S7KeMC1eVY7TsJrvGLo/Mk23EXHuT+Jspc2IhdVuoe8QX7FLHbFsR91yf5bHZF9mOF/Q5fyE/bDjM096KNNYef9UqHr6Xd0bJ6ne9G1ZEMgaoTStzXqHH4bBk12ICKvkQv+Tgb70dGCyIkDwKOhkV4V3QlehwWTDjD0sZtWCT5iA0muNENZa7kDjWpfHR9lVINbafG5gltWrpEPY3NNrvfnrkqKzgkS6phlNDTpDZPkPCYQoIe+7OxmaFoLoto00s+R8jhd4QlRfb6aGw0PSzLajJYztVadVy1mpIsTBPYkTyxoMlUPOW2qclVlrH15LL5GvLyCbI0one0tI9Q5Q5VIaDnyxWgLSzfaLWxs4BuaAeevZIFtzTb0COjskw3c3ghVeJYHhxxtPsWMW48T75h20Zt5UILaeloqKzAo61h1EF2rh6Vyc72db6TFnzQ29nhO8YRrrG7wT86B2m+kxL+aDAsR7EUSRcSXVBNa3ChZ/y2kzLAMKMKDMHWvWMEGE4/gSPQO8ZlcJaMoVJmSAYOKUKGIk9wC4jTZ3DDDMeuUaApk40aWS8b5Gwuh7ONEoo6hpgX8BnVQOB4NskhtlGUWsPQY2R41CDbMhzDyCFnPNzZecV05zrf8WxAMXZHQw30wnYpCmOx8WfFLQVpo9zuD490++lmg0IsDX6JQhxLsEyOJeiINlsxOkINSpajgeLrKb4+g9dSvA5blBQSFB/G2nsVQjtgvc+OW1IqftU2YnmfVsqPh8qI5feV6Nx2/NXfwX2AbxE6mCVna0HHA683aOhDuPM152vWXLJggdVlddVUu6x2K2+32rfz3I40inIfXM7lBtP0iZ7AY/hM2oPPqVmwVp6vMRiANxp1wGfnaPRdflHj1HBmvNVrujTbNUc1FzQ6kddogBChy49PdIYuP+RCfTkU1Zdbc2FBkbNr4823IUimMeOq+QK7Oh7jH7hcxh2+HOSJxn04ve47addh9sAIB9GPCnw6NkCdXKzjiZ7TEq0xS8sLvNcvmIkOdF4/Pk2jHXAVsbsaIhqhVuqIvc5eQOwFB7mnL2/nWy/fxL2+iy/dveuzf9uNQd89/p7gEVbh03cxtMkVRQA5Wt30vDxdDm+bUQRef1GR0WIp8PotFiNavKC9pOWG0QWtsRDqXc6bb54S49T4aIQkv9BVO/+GaSbimM1ZLbmu2lxrAZmt1dk50vC9Pf0PF/9DxbuPv5f+67vvfpQuueewhmueQf77H3/mX1l5+12klOSSLCKm305fKCJvHn2INOPjLexP+4RZQgvYwQmr5XKB58uss6cZDKJVrK6xmfNLvP5p+RZThddvNBXQ3EhCtcAJAtigvtbJvHVN3iabIfNFj2eXXnfDLOKqtdY5rnhdOM01b/4NLm2BNV+bN6/UMVtbkE+ZlhCu/6lzM8ast234C1fzwy0vn/jpuduerOT1wjPat+z337lrm2sg0LnDk/aN7Jjespp87Sf9txAe29lGsiKBWfuz5x/57OXf/Z5//ce/OXPhgaPerhOZmjek1wq72BvRAtmWazBxJqPFmmU0WgsKTQaDxmI0gwaLbss0mCt3gdM1GUkuKz2N5Lo6mv16QlykcNoNeDcRMmdFbWlV2+7q3PT1Z4l+vW4umX86faP/THpt1r3aTTtqBOflb16cFeVz//7yu6eZL6fHP+T/qunADpsv23AfcPn55sJp1myv31qoR7rXryE8T8y0GayuiSac7MCa6rw6V16m1Wk33FCgdcwurbOePrJwC1HS3s7APY8//cRjj/HP7iPF6T/su5xqa529q2rXIe6RTC6exP6cg/UuhVXy9TqtmFc8PRumQ55WuK5MzC7kC2diJorjxVwWX1xcaOGNXr9Ox7PeZMmhG4+154LPNSf1hFVbqptXet2cKlI3bz4ttq4KK1+QXyiSWZww508/+9kv7Y/kfeMBYuoJpf+yr/WtV5U3ix/L2rL5k/YNmx/fv4bUfefojt3iTW3PyG3Tl66ItR984u7t+c0rHljUXCiWrRrKxDGC+7gF31WKwCUXFxKi5bic6cVGK/YpUjSC11+oMRPcx/VflERidVhxG6sOFlAHTWQmbmqu6UfpvxHtj3/b/OT1s044w7fUkHf5Zz/rwHxOf+3ZHP19muyq8M3GffiGM04dEc5pv5tbiqcaWHX0vwn4GPLkLM6kKeWgqETQlZDyOsAvfZXM8OMZqIMcaJevz+L4bAJajV4vAOZYEMwmHeGyuC5/dlbWOj1p0RO9VsML9OSrrXe5br4ZG5MF46SxWHFXYXtiRNij+K2ptvN23kFcBmImCAnGkcuv7fopSf+KfHL5cLb7AfL6c+Sb6Ts07r+9KDx/3VtpP/k4k8txYZQ/p3ka28ApTzcYC6cZpxXbCk0mzX4/mPash7z9fgMenPW15eVTzsPM/q7iaOp0jiWcq3YWR48nl4nw3PUd3pWO6bPys2JZzjX1FR3eFfaSMmPc0iuMllSW5M2Ru3vmI+BsHomy3HB8+lPuVdyj9HemUs7DE4bX6fQGwN8bnfa763VmfoyYsJrq0ZhJQMYHV54jr8BRx9kOFf305Z9wz322XNP06quY76H0Wr4Je8SCO3++PMOajz9F2drsgsJca7s/F8wmr99s5g1eP69uffXsVcOjyjWZrmZbv462zHV1rgK+6eLrbd+vvP/rwyPpCNfyyiszXnyz2Lpn9l2b+X/e9+bZszSn92CtN6BtA1TIhYS2pMaYpcfzU48wj+3JT/mNuRJMCW7sOjs1xF0kt392PXkifYH8Yt++fYKyj9WK9ZHzzKM/7zIv+oQTM/+/nDs4c9mVN3g87bArYfLPmYyc9unLD015zSfXvPYT4TX8rX+M/j7C3bAfGuA0PEl3GV7jHA9DNCK85kAYHsTPh6SHPEX+yLVy+7gnuI/4efxG/jD/iqrZAtXoZxlWk0PYCRvwKeIkb8U1pc4i0Un7N036QsCMqwzMYReEVJjHX9IBFRaQ5x4V1oAJvq3CWoQfV2EdbINRFdZDPilXYQOYSL0KG0mSrFThLJjBnZ38d7GKO6/COVDHG1XYBMV8PfVewI6EZ3m/ChOYJWhUmAOT4FBhHuYJNSosIE9IhTUwQ7hThbUIP6LCOvhYeFGF9VCmOarCBpih+aUKG7k/aP6swllwo/5XKpwNGwxWFc6BWwyDKmyCeYZfNkX6I6nItlBQCgZSAak3Ft+aiPSHU1JZ71yptrqmWloWi/UPhKTGWCIeSwRSkVi0yth4LVuttAZVNAdSFdLyaG9Va6QnlOGVVsaisTWh/qGBQGJpsjcUDYYSUqV0DcM1y5tCiSSFa6uqq6tqrhCvYY0kpYCUSgSCocFA4lYp1ne1E1Ii1B9JpkIJREaiUmdVe5XkDaRC0ZQUiAaljknBtr6+SG+IIXtDiVQAmWOpMPp5y1AikgxGeqm1ZNWk+1NS0Z4KbQpJKwOpVCgZizYEkmgLPWuMDSUj0VCFtDkc6Q1LmwNJKRhKRvqjSO7ZKl0tJSE1gNFEo7FNqHQTiiVCfYlQMhyJ9kvJQDQpJUOJSJ+qQkqFAyka+2AolYj0BgYGtmLZBuMo2oN12hxJhan9RAQ9XRXafKRqwhtMUB8mVooMxhOxTczRymRvIhSKor1AMNATGYikUFc4kAj0Ytowd5HeJEsLZkOKB6KV7qFELB5CZ9cua73CiO5lUpqMDWwKJRl3NBQKJmlJghjqAAqh4YFY7FYaUl8sgW4GU+HKKX73xaIpFI1JgWAQY8eExXqHBmmxMNepCecCvYkY0uIDgRRqGUxWhVOp+EKnc/PmzVUBtT69WJ4q1Oz8KlpqazykliRBtQwOtGIPRGn9hliRaRDty1ultjjmx4POSSpDhTTRnjVVNaoJTGMknkpWJSMDVbFEv7PN0wpNEIF+HCkc2/CwCoKEI4DrAEK9EIM4bIUE4wojVsLjsBfm4lyLh2MNDgmWIVcM6QMoL0EjwgmUovcA0xuDKFSBkVG+WlstQmtUL5qZdAVCy1G+FzW0olwPUqfqlWAlm2NMrh8P+AGkJmApJFEmhJQgk5CgEsdXa/hq6k2MkpzE16JH1fipQr+/SPKrtUZQk8RynGIU6uUg8/xWxMWg7yszISFfiNUtiZQQWwWZVqq7EznaGZeXSdIspJi1KOPq+AKLbWixD+V7WQ0nOHuZbtoLGc0xhMNqPm/BXCeYB0EmNxFbEi1/Pvtf3BXtzLtNzOZKhqfrJKM14DqpxpXJGdUxxCoQRTzNx2b0htoOMzjAchpkGmiHRVXpHuw56SttSapsQK1NlFVuk+rpJtUazXIfuyeZ3SjakBAOsKgl5i3NSN81XkgsawFWg0zdB5GaYry9iB/Az1Z1tw1ijjJWe9T9tJntzvBk/FQqk9NVOG+2z2aVvjo3mQ7qUzuWWqV6EyymKxmtZFWi8YSYlxQKsN3fgxIDzG7GrzDrkwCrckiteop5P5G1oBoltR1nmEpwM2/png+pmV2LZ0XrF2rMZG9ql9LKDDB/k1N0R5m3QYaLTWaacg2oljIRD7Az6dbJKvWxzstkM8i0VX5JvvtYblKq1RjzKIifTN0zHRZD2SFWxczOyvR16nOZC7D8xlS5ODubUqovg2ynhFkfxmEhPl460Tv6qWLdOHX/9Kq7p0r12fm/lqN+xVkGp+6SxKQvg+hjq3oORCf339CUnTxRiXY8jVrZyRFX+8ejZk66RgPdO9eenjXs3Lw6ikw3RnCdYv4kWS6rWAz9SG9DC62ZZ+nMG4IDOuALrqWlpB0IPhl3kjXqfBPpwLcnkXTiLOLcBi6yCvGtOFP6YlhMFuG8CPkX4vw1XNO5jsw7NizC0ioyDyw4ODaqkOKCZlKLR+0w3gmODLYG5aoRa8Y7wZHBOhGLM0h478aB7z54lxhkIFXHCHSOkcpji+lUcRzGxfhSK2lCBXQsQQWNqKAB5wZ1XY/rJXJ/J1wmn3jLxI88ZeJ/ea4XP/TUifs/eOSDox/wsUv7L3FnLpFHLxHxUtel2CUe3pPf44zvesbF/3inVPzDO4vF378zSzS/Q2b+7m2PaH6byG97CsXfXvSIZy6+fvHCRV6+6JrvuegpEk+RfFhCctFunpy9mO+8sPg3nf+++HwnLM0lhegRHQUY3lG8EwyrALw4OKB/XBBildv5cfE35HyndN57fvi8cl4wnydvFLjErpdiL21/iT/zE/Jjb6kYP02k09Wnz57m46eHT3PmU+Ipznmq/lTs1NFTF05pTj5XKkpj1WPesfjY8JhmbPysPGMsb67HcoJIJ7wnhk8oJ4Th55XnOfPx+uOXjuN7do5cfqRZHFYOKJyinFXeUHjn0fqj3KPPKc9xZ5974znO+Wz9s9wjz5CzR944wi3NIWaoxZfzTiyOCYttwkhM2GpmYpELiPdw9+H4Yf6h+0vFBz2lYvUD8gMc+nD8/sIZHuqL4X6T1fO9Q4vER5caiBsWYY8tU2cPcctlQfHbtnHRfOjooTOHePnQzBqPfKjQhrdss8d80Hmw/uD2g5cOaswvkGyIkWxZ4r61t1S8r31cvHCAVB8g4gHnAS52YPsBDvZb9kv7eWpU2l80wyPtq97Hte3t2hvby1fvIeY94h7nHl7eY8nzWM6QLIwiC6px8ONnSdaxaZLnJAVkryXfs/uOUnHXikXiznsXi/fetUi8Z8W4+MjdxHKXdFf1XXz1nWT7HUS+w5DtSWJ9YthcURzFpKhzuquoU+fiO7VY2W6kdeE4OX6R6I6JpR4GyGLeDM/Gdc3iBk+NuB7ndTjn1eZ2agjfKdTy2On6522LRDNPTpLppOhYnSiP4TStzDNGjHIJKlzjtYmXVo+v5uTVdTd65NUlZZ7XveRCK2n1zBRbPM2id4zY5B6yAuuxHB1rxrEMx1EPueC55OGGPWQaKegsrC3otBJzp6XW3MnhTiO4v2bYgqJorjd3mbebBbPZaW4zx8z7zRfM42ZdPeIumfkY4CFBHi0kGjJGDox2tJeXt4zpxte0KAbveoXsVEra6V1evU7R7lSgc9163ygh+/x3790LDTNblNp2n9I909+iBBGQKTCMgGXmaCE0+JOpZGqoPHMRFUxCeXkqhTNbMAoOKJ+4CF2Q8mQqlVQxKIGrVPkQu5cnkxOClBcBQDOoPomnKQqlypMEf4dwQilqFKVJCphYEm8TJlHTxmQ5bEyy5UYUQQ3JjC+Tvm1MZjxNTlhkVxHA/wB0IZqkCmVuZHN0cmVhbQplbmRvYmoKCjYgMCBvYmoKNTk2MAplbmRvYmoKCjcgMCBvYmoKPDwvVHlwZS9Gb250RGVzY3JpcHRvci9Gb250TmFtZS9CQUFBQUErTGliZXJhdGlvbk1vbm8KL0ZsYWdzIDUKL0ZvbnRCQm94Wy00ODEgLTMwMCA3NDEgOTgwXS9JdGFsaWNBbmdsZSAwCi9Bc2NlbnQgODMyCi9EZXNjZW50IC0zMDAKL0NhcEhlaWdodCA5ODAKL1N0ZW1WIDgwCi9Gb250RmlsZTIgNSAwIFIKPj4KZW5kb2JqCgo4IDAgb2JqCjw8L0xlbmd0aCAyODIvRmlsdGVyL0ZsYXRlRGVjb2RlPj4Kc3RyZWFtCnicXZHLboMwEEX3/gov00XEM9BICIkSRWLRh0rzAcYeqKViLGMW/H3tcdpKXYDOMPfaw52o7S6dkjZ6MwvvwdJRKmFgXTbDgQ4wSUWSlArJ7b3CN5+ZJpHz9vtqYe7UuFQVid5db7Vmp4dGLAM8kOjVCDBSTfRwa3tX95vWXzCDsjQmdU0FjO6cZ6Zf2AwRuo6dcG1p96Oz/Ak+dg00xToJo/BFwKoZB8PUBKSK45pW12tNQIl/vSQLlmHkn8w4aeKkcZyfascpctl4zpDT2HOOXKDmFLj0XAT92XMZOPf8GDjzfA76wnOD3OL3J+Qm8dwGDd57Cdzi8Pcp/W/4nH/ioXwzxkWDy8BMfBpSwe++9KK9C59v5JuJyAplbmRzdHJlYW0KZW5kb2JqCgo5IDAgb2JqCjw8L1R5cGUvRm9udC9TdWJ0eXBlL1RydWVUeXBlL0Jhc2VGb250L0JBQUFBQStMaWJlcmF0aW9uTW9ubwovRmlyc3RDaGFyIDAKL0xhc3RDaGFyIDEzCi9XaWR0aHNbNjAwIDYwMCA2MDAgNjAwIDYwMCA2MDAgNjAwIDYwMCA2MDAgNjAwIDYwMCA2MDAgNjAwIDYwMCBdCi9Gb250RGVzY3JpcHRvciA3IDAgUgovVG9Vbmljb2RlIDggMCBSCj4+CmVuZG9iagoKMTAgMCBvYmoKPDwvRjEgOSAwIFIKPj4KZW5kb2JqCgoxMSAwIG9iago8PC9Gb250IDEwIDAgUgovUHJvY1NldFsvUERGL1RleHRdCj4+CmVuZG9iagoKMSAwIG9iago8PC9UeXBlL1BhZ2UvUGFyZW50IDQgMCBSL1Jlc291cmNlcyAxMSAwIFIvTWVkaWFCb3hbMCAwIDU5NS4yNzU1OTA1NTExODEgODQxLjg2MTQxNzMyMjgzNV0vR3JvdXA8PC9TL1RyYW5zcGFyZW5jeS9DUy9EZXZpY2VSR0IvSSB0cnVlPj4vQ29udGVudHMgMiAwIFI+PgplbmRvYmoKCjQgMCBvYmoKPDwvVHlwZS9QYWdlcwovUmVzb3VyY2VzIDExIDAgUgovTWVkaWFCb3hbIDAgMCA1OTUgODQxIF0KL0tpZHNbIDEgMCBSIF0KL0NvdW50IDE+PgplbmRvYmoKCjEyIDAgb2JqCjw8L1R5cGUvQ2F0YWxvZy9QYWdlcyA0IDAgUgovT3BlbkFjdGlvblsxIDAgUiAvWFlaIG51bGwgbnVsbCAwXQovTGFuZyhlbi1VUykKPj4KZW5kb2JqCgoxMyAwIG9iago8PC9DcmVhdG9yPEZFRkYwMDU3MDA3MjAwNjkwMDc0MDA2NTAwNzI+Ci9Qcm9kdWNlcjxGRUZGMDA0QzAwNjkwMDYyMDA3MjAwNjUwMDRGMDA2NjAwNjYwMDY5MDA2MzAwNjUwMDIwMDAzNTAwMkUwMDM0PgovQ3JlYXRpb25EYXRlKEQ6MjAxOTA5MTExMDU4NTJaJyk+PgplbmRvYmoKCnhyZWYKMCAxNAowMDAwMDAwMDAwIDY1NTM1IGYgCjAwMDAwMDcxMjUgMDAwMDAgbiAKMDAwMDAwMDAxOSAwMDAwMCBuIAowMDAwMDAwMTk4IDAwMDAwIG4gCjAwMDAwMDcyOTQgMDAwMDAgbiAKMDAwMDAwMDIxOCAwMDAwMCBuIAowMDAwMDA2MjYyIDAwMDAwIG4gCjAwMDAwMDYyODMgMDAwMDAgbiAKMDAwMDAwNjQ3NiAwMDAwMCBuIAowMDAwMDA2ODI3IDAwMDAwIG4gCjAwMDAwMDcwMzggMDAwMDAgbiAKMDAwMDAwNzA3MCAwMDAwMCBuIAowMDAwMDA3MzkzIDAwMDAwIG4gCjAwMDAwMDc0OTAgMDAwMDAgbiAKdHJhaWxlcgo8PC9TaXplIDE0L1Jvb3QgMTIgMCBSCi9JbmZvIDEzIDAgUgovSUQgWyA8RUMzNkI1RkFENDBGREE2M0VBNjhEMzZDQTU3OTQyRDY+CjxFQzM2QjVGQUQ0MEZEQTYzRUE2OEQzNkNBNTc5NDJENj4gXQovRG9jQ2hlY2tzdW0gL0ZCRkQyQThGMjgwNEM0RjAxQzRCRDgxNDVBOTJFN0E3Cj4+CnN0YXJ0eHJlZgo3NjYwCiUlRU9GCg=="
    }
}
```

#### Response

```json
{
    "filePath": "srattached/image.jpg",
    "type": "image"
}
```

## 2. lépés

Ezt követően az előbb feltöltött képhez a [Document resource](https://www.shoprenter.hu/api/doc#document) segítségével egy azonosítót hozunk létre, amit legkönnyebben az alábbi request elküldésével tudunk megkapni.

### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/documents</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": []
}
```

#### Response

```json
{
    "href": "http://shopname.api.shoprenter.hu/documents/ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ==",
    "id": "ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ==",
    "innerId": "5",
    "dateCreated": "2019-09-11T15:12:47",
    "dateUpdated": "2019-09-11T15:12:47"
}
``` 

## 3. lépés

A Document resource ID birtokában, a [Document Description resource](https://www.shoprenter.hu/api/doc#document_description) segítségével beállíthatjuk a feltöltött dokumentum nevét és nyelvét. A nyelvet a [Language resource](https://www.shoprenter.hu/api/doc#language) segítségével tudjuk lekérdezni. Megjegyzés: a **filename** és a **mask** értékének nem kell megegyezni.

### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/documentDescriptions</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": {
        "name": "Kép neve",
        "filename": "image.jpg",
        "mask": "image.jpg",
        "document": {
            "id": "ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ=="
        },
        "language": {
            "id": "bGFuZ3VhZ2UtbGFuZ3VhZ2VfaWQ9MQ=="
        }
    }
}
```

#### Response

```json
{
    "href": "http://shopname.api.shoprenter.hu/documentDescriptions/ZG9jdW1lbnREZXNjcmlwdGlvbi1kb2N1bWVudF9pZD01Jmxhbmd1YWdlX2lkPTE=",
    "id": "ZG9jdW1lbnREZXNjcmlwdGlvbi1kb2N1bWVudF9pZD01Jmxhbmd1YWdlX2lkPTE=",
    "name": "Pdf Dokumentum szövege",
    "filename": "test.pdf",
    "mask": "test.pdf",
    "document": {
        "href": "http://shopname.api.shoprenter.hu/documents/ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ=="
    },
    "language": {
        "href": "http://shopname.api.shoprenter.hu/languages/bGFuZ3VhZ2UtbGFuZ3VhZ2VfaWQ9MQ=="
    }
}
```

## 4. lépés

Ha mindez megvan, akkor a [Product Document Relation resource](https://www.shoprenter.hu/api/doc#product_document_relation) segítségével a kívánt termékhez tudjuk csatolni a feltöltött dokumentumot. A terméket a [Product resource](https://www.shoprenter.hu/api/doc#product) segítségével tudjuk lekérdezni. 

### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/productDocumentRelations</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": {
        "product": {
            "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ=="
        },
        "document": {
            "id": "ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ=="
        }
    }
}
```

#### Response

```json
{
    "href": "http://shopname.api.shoprenter.hu/productDocumentRelations/cHJvZHVjdERvY3VtZW50LWlkPTY=",
    "id": "cHJvZHVjdERvY3VtZW50LWlkPTY=",
    "product": {
        "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ=="
    },
    "document": {
        "href": "http://shopname.api.shoprenter.hu/documents/ZG9jdW1lbnQtZG9jdW1lbnRfaWQ9NQ=="
    }
}
```
