<script>
import fabricObject from "./fabricObject";
export default {
  name: "fabric-polyline",
  mixins: [fabricObject],
  props: {
    points: {
      type: Array,
      default: function() {
        return [
          { x: 10, y: 10 },
          { x: 50, y: 30 },
          { x: 40, y: 70 },
          { x: 60, y: 50 },
          { x: 100, y: 150 },
          { x: 40, y: 100 }
        ];
      }
    },
    stroke: { type: String, default: "red" }
  },
  data() {
    return {
      polyline: null,
      type: "polyline"
    };
  },
  render(h) {
    return this.$slots.default ? h("div", this.$slots.default) : undefined;
  },
  watch: {
    parentItem: {
      handler(newValue) {
        if (newValue) {
          //Parent is created
          this.polyline = new this.fabric.Polyline(this.points, {
            ...this.definedProps
          });
          if (this.parentType == "group") {
            if (this.parentItem.addWithoutUpdate) {
              this.parentItem.add(this.polyline);
            } else {
              this.parentItem.addWithUpdate(this.polyline);
            }
          } else {
            this.canvas.add(this.polyline);
          }
          this.createEvents();
          this.createWatchers();
        }
      },
      immediate: true
    }
  },
  methods: {},
  beforeDestroy() {}
};
</script>
