export default function copyToClipboard(input: any): boolean {
  let value!: string

  if (typeof input !== "string") {
    try {
      value = JSON.stringify(input)
    } catch (e) {
      throw "Failed to copy value to clipboard. Unknown type."
    }
  } else {
    value = input
  }

  const textarea = document.createElement("textarea")

  textarea.value = value
  textarea.setAttribute("readonly", "")
  textarea.style.cssText = "position:fixed;pointer-events:none;z-index:-9999;opacity:0;"

  document.body.appendChild(textarea)

  /* Must use range selection method if browser running on iOS */
  if (navigator.userAgent.match(/ipad|ipod|iphone/i)) {
    textarea.contentEditable = "true"
    textarea.readOnly = true

    const range = document.createRange()

    range.selectNodeContents(textarea)

    /* Get the range created above */
    const selection = window.getSelection()!

    selection.removeAllRanges()
    selection.addRange(range)
    textarea.setSelectionRange(0, 999999)
  } else {
    textarea.select()
  }

  let success = false

  try {
    success = document.execCommand("copy")
  } catch (err) {
    console.warn(err)
  }

  document.body.removeChild(textarea)

  return success
}
