<template>
  <div class="omegaup-user-roles panel-primary panel">
    <div class="panel-heading">
      <h2 class="panel-title">{{ T.omegaupTitleUpdatePrivileges }}</h2>
    </div>
    <div class="panel-body">
      <h4>{{ T.userRoles }}</h4>
      <table class="table">
        <tbody>
          <tr v-for="role in roles">
            <td>
              <input
                v-model="role.value"
                type="checkbox"
                @change.prevent="onChangeRole($event, role)"
              />
            </td>

            <td>{{ role.name }}</td>
          </tr>
        </tbody>
      </table>
      <h4>{{ T.userGroups }}</h4>
      <table class="table">
        <tbody>
          <tr v-for="group in groups">
            <td>
              <input
                v-model="group.value"
                type="checkbox"
                @change.prevent="onChangeGroup($event, group)"
              />
            </td>

            <td>{{ group.name }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop, Emit } from 'vue-property-decorator';
import { omegaup } from '../../omegaup';
import T from '../../lang';

@Component
export default class AdminRoles extends Vue {
  @Prop() initialRoles!: omegaup.Role[];
  @Prop() initialGroups!: omegaup.Group[];

  T = T;
  roles: omegaup.Role[] = this.initialRoles;
  groups: omegaup.Group[] = this.initialGroups;

  @Emit()
  onChangeRole(
    ev: Event,
    role: omegaup.Role,
  ): omegaup.Selectable<omegaup.Role> {
    return {
      value: role,
      selected: (<HTMLInputElement>ev.target).checked,
    };
  }

  @Emit()
  onChangeGroup(
    ev: Event,
    group: omegaup.Group,
  ): omegaup.Selectable<omegaup.Group> {
    return {
      value: group,
      selected: (<HTMLInputElement>ev.target).checked,
    };
  }
}
</script>
